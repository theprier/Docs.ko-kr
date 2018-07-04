---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: 제공 CRUD (만들기, 읽기, 업데이트, 삭제) 데이터 양식 항목 지원 | Microsoft Docs
author: microsoft
description: 5 단계 편집, 만들기 및도 함께 Dinners 삭제에 대 한 지원 사용 하 여 추가로 DinnersController 클래스를 사용 하는 방법을 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: 821684c0753967fc1a693b061d5d539951cd7c23
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388810"
---
<a name="provide-crud-create-read-update-delete-data-form-entry-support"></a>제공 CRUD (만들기, 읽기, 업데이트, 삭제) 데이터 양식 항목 지원
====================
[Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 5 단계 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 5 단계 편집, 만들기 및도 함께 Dinners 삭제에 대 한 지원 사용 하 여 추가로 DinnersController 클래스를 사용 하는 방법을 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a>NerdDinner 5 단계: 만들기, 업데이트, 양식 시나리오를 삭제 합니다.

컨트롤러 및 보기를 도입 하 고 사용 하 여 사이트에서 Dinners에 대 한 목록/세부 정보 환경을 구현 하는 방법을 설명 했습니다. 다음 단계는 DinnersController 클래스를 좀 더 수행 하 고 편집, 만들기 및도 함께 Dinners 삭제에 대 한 지원을 사용 하도록 설정 해야 합니다.

### <a name="urls-handled-by-dinnerscontroller"></a>DinnersController에서 처리 하는 Url

두 Url에 대 한 지원을 구현 하는 DinnersController에 작업 메서드 이전에 추가한: */Dinners* 하 고 */Dinners 세부 정보 / [id]* 합니다.

| **URL** | **동사** | **용도** |
| --- | --- | --- |
| */Dinners/* | 가져오기 | 예정 된 dinners는 HTML 목록을 표시 합니다. |
| */Dinners/Details/[id]* | 가져오기 | 특정 저녁에 대 한 정보를 표시 합니다. |

이제 세 가지 추가 Url을 구현 하는 작업 메서드를 추가 합니다. <em>/Dinners/편집 / [id], Dinners/만들기,</em>하 고<em>/Dinners/삭제 / [id]</em>합니다. 이러한 Url 편집 기존 Dinners 새 Dinners 만들고 Dinners 삭제에 대 한 지원을 사용 하도록 설정 됩니다.

이러한 새 Url 사용 하 여 HTTP GET 및 HTTP POST 동사 상호 작용 지원할 예정입니다. 다음이 Url에 HTTP GET 요청 데이터 (폼 데이터로 Dinner "편집"의 경우, "만들기"의 경우 빈 폼 및 삭제 확인 화면이 "삭제"의 경우)의 초기 HTML 보기를 표시 됩니다. 다음이 Url에 HTTP POST 요청 우리의 DinnerRepository (그리고 데이터베이스에는 여기에서) Dinner 데이터를 저장/업데이트/삭제 됩니다.

| **URL** | **동사** | **용도** |
| --- | --- | --- |
| */Dinners/Edit/[id]* | 가져오기 | 저녁 식사 데이터로 채워진 편집 가능한 HTML 폼을 표시 합니다. |
| 올리기 | 데이터베이스에 특정 저녁 폼 변경 내용을 저장 합니다. |
| */Dinners/Create* | 가져오기 | 사용자가 새 Dinners 정의할 수 있는 빈 HTML 폼을 표시 합니다. |
| 올리기 | 새 Dinner 만들고 데이터베이스에 저장 합니다. |
| */Dinners/Delete/[id]* | 가져오기 | 삭제 확인 화면을 표시 합니다. |
| 올리기 | 데이터베이스에서 지정한 저녁 식사를 삭제합니다. |

### <a name="edit-support"></a>편집 지원

"편집" 시나리오를 구현 하 여 시작 해 보겠습니다.

#### <a name="the-http-get-edit-action-method"></a>HTTP GET 편집 작업 메서드

편집 작업 메서드는 HTTP "GET" 동작을 구현 하 여 시작 하겠습니다. 이 메서드에서 될 때 호출 된 */Dinners/편집 / [id]* URL이 요청 합니다. 구현은 다음과 같습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

위의 코드는 Dinner 개체를 검색 하는 DinnerRepository를 사용 합니다. 그런 다음 Dinner 개체를 사용 하 여 보기 템플릿을 렌더링 합니다. 서식 파일 이름을 명시적으로 전달 하지 않았으므로 합니다 *View()* 도우미 메서드를 보기 템플릿은 해결 하려면 규칙 기반 기본 경로 사용 하면 해당: /Views/Dinners/Edit.aspx 합니다.

이 보기 템플릿은 이제 만들어 보겠습니다. 편집 메서드 내에서 마우스 오른쪽 단추로 클릭 하 고 "추가 보기" 상황에 맞는 메뉴 명령을 선택 하 여이 작업을 수행 합니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

"뷰 추가" 대화 상자 내에서 해당 모델로 보기 템플릿은를 Dinner 개체를 전달 하는 것 및 자동-스 캐 폴드를 "편집" 템플릿을 선택 나타냅니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

"추가" 단추를 클릭 하는 경우 Visual Studio는 "\Views\Dinners" 디렉터리 내에서 새 "Edit.aspx" 보기 템플릿 파일을를에 추가 합니다. 또한 코드-편집기 내 – 초기 "편집" 스 캐 폴드 구현 같은 아래 채워진 새 "Edit.aspx" 보기 템플릿을 열립니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

기본 "편집" 스 캐 폴드 생성에 대 한 몇 가지 변경 하 고 (제거 하는 몇 가지 속성을 노출 하지 않으려는 것) 아래 콘텐츠 보기 템플릿 편집 업데이트 보겠습니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

응용 프로그램 및 요청을 실행할 때 합니다 *"/ 1/편집/Dinners"* URL 페이지를 살펴봅니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

보기에서 생성 된 HTML 태그를 아래와 같습니다. 표준 HTML –를 &lt;폼&gt; HTTP POST를 수행 하는 요소는 */Dinners/Edit/1* URL 때 "저장" &lt;입력 형식 = "제출" /&gt; 단추를 누르면. HTML &lt;입력 형식 = "text" /&gt; 요소는 편집 가능한 각 속성에 대 한 출력 되었습니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a>Html.BeginForm() 및 Html.TextBox() Html 도우미 메서드

"Edit.aspx" 보기 템플릿은 몇 가지 "Html 도우미" 메서드를 사용 하는: Html.ValidationSummary(), Html.BeginForm(), Html.TextBox(), 및 Html.ValidationMessage() 합니다. 미국에 대 한 HTML 태그를 생성 하는 것 외에도 이러한 도우미 메서드는 기본 제공 오류 처리 및 유효성 검사를 지원 합니다.

##### <a name="htmlbeginform-helper-method"></a>Html.BeginForm() 도우미 메서드

Html.BeginForm() 도우미 메서드는 HTML 출력 &lt;폼&gt; 는 태그 요소입니다. Edit.aspx 보기 템플릿은에 적용 중인 C# "using" 문을이 메서드를 사용 하는 경우 알 수 있습니다. 중괄호의 시작을 나타냅니다 합니다 &lt;폼&gt; 콘텐츠 및 닫는 중괄호는 끝을 나타내는 새로운 합니다 &lt;/f&gt; 요소:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

또는 "using" 문을 있다면 다음과 같은 시나리오에 부자연 스러운 접근는 Html.BeginForm() 및 Html.EndForm() 조합 (동일한 작업을 수행)을 사용할 수 있습니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

매개 변수 없이 Html.BeginForm()를 호출 하면 현재 요청의 URL에 HTTP POST를 수행 하는 폼 요소를 출력 합니다. 편집 보기 생성 이유 즉를 *&lt;양식 동작 = "/ Dinners/편집/1" 메서드 "post" =&gt;* 요소입니다. 수 또는 전달 했으므로 명시적 매개 변수가 Html.BeginForm()를 다른 URL에 게시 하려는 경우.

##### <a name="htmltextbox-helper-method"></a>Html.TextBox() 도우미 메서드

Edit.aspx 뷰에 Html.TextBox() 도우미 메서드를 사용 하 여 출력 &lt;type = "text" /&gt; 요소:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

위의 Html.TextBox() 메서드의 i d/이름 특성을 지정 하는 데 사용 되는 단일 매개-변수를 &lt;입력 형식 = "text" /&gt; 에서 텍스트 상자 값을 채우려고 모델 속성 뿐만 아니라 출력 요소. 예를 들어 Dinner 개체 편집 보기에 전달 했습니다 ".NET 미래", "Title" 속성 값 있어 없으므로 Html.TextBox("Title") 메서드 호출 출력: *&lt;입력된 id = "Title" name = "Title" type = "text" value = ".NET 미래" /&gt;*.

또는 요소의 id/이름을 지정 하 고 두 번째 매개 변수로 사용할 값에 명시적으로 전달 하려면 첫 번째 Html.TextBox() 매개 변수를 사용할 수 것:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

종종 출력 되는 값에 사용자 지정 형식 지정을 수행 하려고 합니다. .NET에 기본 제공 string.format () 정적 메서드가 이러한 시나리오에 유용합니다. Edit.aspx 보기 템플릿은 형식을 지정 하 여이 EventDate 값 (날짜/시간 형식입니다.) 시간을 초를 표시 하지 않습니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

필요에 따라 Html.TextBox()는 세 번째 매개 변수 추가 HTML 특성을 출력에 사용할 수 있습니다. 아래 코드 조각에는 추가 크기를 렌더링 하는 방법을 보여 줍니다. "30" 특성과 class = = "mycssclass" 특성에는 &lt;type = "text" /&gt; 요소입니다. 확인 하는 방법을 사용 하 여 클래스 특성의 이름을 이스케이프 된 것을 "@" character because "클래스"는 C#에서 예약 된 키워드:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a>HTTP POST 편집 작업 메서드를 구현합니다.

이제 구현 하는 편집 작업 메서드를 HTTP GET 버전이 있습니다. 사용자가 요청 하는 경우는 */Dinners/Edit/1* 다음과 같은 HTML 페이지를 받은 URL:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

"저장" 단추를 누르면 폼 post를 실행 하는 */Dinners/Edit/1* URL을 HTML 제출 &lt;입력&gt; HTTP POST 동사를 사용 하 여 값을 형성 합니다. 이제는 편집 작업 메서드의 – Dinner 저장를 처리 하는 HTTP POST 동작을 구현 해 보겠습니다.

HTTP POST 시나리오 처리 여부를 나타내는 "AcceptVerbs" 특성에는 우리의 DinnersController 오버 로드 "편집" 작업 메서드도 추가 시작 합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

오버 로드 된 작업 메서드에 [AcceptVerbs] 특성이 적용 되 면 ASP.NET MVC는 자동으로 들어오는 HTTP 동사에 따라 적절 한 동작 메서드에 디스패치 요청을 처리 합니다. HTTP POST 요청을 <em>/Dinners/편집 / [id]</em> Url에 다른 모든 HTTP 동사 요청 하는 동안 위의 편집 메서드를 이동 <em>/Dinners/편집 / [id]</em>Url 될 첫 번째 편집 메서드에 구현 했습니다 (않았습니다 있음 없습니다 [AcceptVerbs] 특성).

| **HTTP 동사를 통해 쪽 항목: 이유 구분?** |
| --- |
| 궁금할 – 단일 URL을 사용 하 고 HTTP 동사를 통해 해당 동작을 구분 했습니다 이유는 무엇 인가요? 편집 변경 내용 저장 및 로드를 처리 하는 두 개의 별도 Url을 방금 하면 안 되나요? 예를 들어: /Dinners/편집 / [id] 초기 폼과 /Dinners/저장 / [id] 저장 하는 폼 게시를 처리 하도록 표시할? 두 개의 별도 Url 게시를 사용 하 여 단점은 경우 여기서 /Dinners/Save/2를 게시 하 고 HTML 폼 입력된 오류로 인해 다시 표시 해야 합니다 (이후에 브라우저의 주소 표시줄에 Dinners/저장/2 URL을 보유 하는 최종 사용자가 종료 됩니다. URL 형식에 게시). 최종 사용자가 해당 브라우저 즐겨찾기 목록에이 redisplayed 페이지 책갈피를 설정 하거나 URL 복사/붙여 넣습니다. 및 친구에 게 하는 경우 (해당 URL 게시 값에 따라 다름) 때문에 나중에 작동 하지 않는 URL을 저장 결국 것입니다. 단일 URL을 노출 하 여 (같은: 최종 사용자가 편집 페이지를 책갈피 및/또는 다른 사용자에 게 URL을 보냅니다 괜찮습니다 /Dinners/Edit/[id]) 및 HTTP 동사에서의 처리를 구분 합니다. |

#### <a name="retrieving-form-post-values"></a>폼 게시 값 검색

다양 한 폼 매개 변수는 HTTP POST "편집" 메서드 내에서 게시 방법 액세스할 수 있습니다. 한 가지 간단한 방법은 방금 폼 컬렉션에 액세스 하 여 게시 된 값을 직접 검색할 컨트롤러 기본 클래스에서 요청 속성을 사용 하는 것입니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

위의 방법은 다소 복잡 하지만 오류 처리 논리를 추가 하는 면에 특히 합니다.

이 시나리오는 기본 제공을 활용 하는 방식이 더 효과적 *UpdateModel()* 컨트롤러 기본 클래스에서 도우미 메서드입니다. 들어오는 폼 매개 변수를 사용 하 여 전달 하는 개체의 속성 업데이트를 지원 합니다. 리플렉션을 사용 하 여 개체의 속성 이름을 확인 하 고 자동으로 변환 하 고에 클라이언트에서 제출한 입력된 값에 따라 값을 할당 합니다.

이 코드를 사용 하 여 HTTP POST 편집 작업을 간소화 하기 위해 UpdateModel() 메서드를 사용 수 있습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

이제 방문할 수는 */Dinners/Edit/1* URL 및 우리의 Dinner의 제목 변경 합니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

"저장" 단추를 클릭 하면 폼이 편집 작업을 수행 하겠습니다 및 업데이트 된 값이 데이터베이스에 유지 됩니다. 에서는 다음 리디렉션됩니다 정보 URL (새로 저장된 된 값이 표시 됩니다)는 저녁에:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a>편집 오류 처리

경우는 제외 –는 현재 HTTP POST 구현 작업이 제대로 수행 오류가 있습니다.

사용자 양식 편집 실수를 하면 폼은 해결 하도록 안내 하는 오류 정보 메시지와 함께 다시 표시 되도록 해야 합니다. 최종 사용자가 잘못 된 입력을 게시 하는 위치 하는 경우가 포함 됩니다 (예: 잘못 된 형식의 날짜 문자열로) 처럼 입력된 형식이 유효 인 사례와 이지만 비즈니스 규칙 위반을 합니다. 오류가 발생 한 경우 양식에 사용자가 해당 변경 내용이 수동으로 충전 필요가 있도록 원래 입력 한 입력된 데이터를 유지 해야 합니다. 이 프로세스는 폼이 성공적으로 완료 될 때까지 필요한 횟수 만큼 반복 해야 합니다.

ASP.NET MVC 오류 처리 및 양식 다시 쉽게 하는 몇 가지 유용한 기본 제공 기능이 포함 됩니다. 작업에서 이러한 기능을 보겠습니다 보려는 편집 작업 메서드를 다음 코드로 업데이트 합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

위의 코드는 작업 주변 try/catch 오류 처리 블록에 배치 된 것을 제외 하 고 이전 구현-와 비슷합니다. 예외가 발생 한 경우 UpdateModel()를 호출 하는 경우 또는 시도 하 고 (저장 하려고 Dinner 개체 모델 내에서 규칙 위반으로 인해 올바르지 않으면 예외가 발생 합니다)는 DinnerRepository를 저장 하는 경우이 catch 오류 처리 블록이 됩니다. 실행 합니다. 그 Dinner 개체에 있는 모든 규칙 위반을 반복 하 고 (곧 설명 하겠습니다)는 ModelState 개체에 추가 합니다. 에서는 다음 뷰가 다시 표시합니다.

이 확인 하려면 응용 프로그램을 다시 실행 해 보겠습니다 작업 저녁을 편집한 빈 제목을, "BOGUS"의 EventDate 있고 미국 국가 값을 사용 하 여 영국 전화 번호를 사용 하도록 변경 합니다. "저장" 단추를 누르면에서는 HTTP POST 편집 메서드를 사용 하 여 하지 못하게 됩니다 (오류가 있기 때문에)를 저녁 식사를 저장 하 고 양식을 다시 표시 됩니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

응용 프로그램에는 훌륭한 오류 환경이 있습니다. 잘못 된 입력이 포함 된 텍스트 요소는 빨간색으로 강조 표시 하 고 유효성 검사 오류 메시지에 대 한 최종 사용자에 게 표시 됩니다. 도 폼은 충전 아무 것도 하지 않아도 되도록 사용자가 입력 한 원래 – 입력된 데이터를 유지 해야.

방법 인지 궁금할이 발생 했습니까? 어떻게 않았습니다 EventDate, 제목과 ContactPhone 텍스트 상자 자체를 빨간색으로 강조 표시 하 고 원래 입력 한 사용자 값을 출력 하도록 알고? 및 어떻게 않았습니다 오류 메시지 표시 맨 위에 있는 목록에서? 좋은 소식은 마법의이 발생 하지 않은-대신가 쉽게 입력된 유효성 검사 및 오류 처리 시나리오는 기본 제공 ASP.NET MVC 기능 중 일부를 사용 하기 때문입니다.

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a>ModelState 이해 및 유효성 검사 HTML 도우미 메서드

컨트롤러 클래스에는 오류를 보기에 전달 되는 모델 개체를 사용 하 여 없음을 표시 하는 방법을 제공 하는 "ModelState" 속성 컬렉션을 있습니다. ModelState 컬렉션 내에서 오류 항목 문제를 사용 하 여 모델 속성의 이름을 식별 (예를 들어: "Title", "EventDate" 또는 "ContactPhone")를 지정 친숙 한 오류 메시지를 허용 하 고 (예: "Title이 필요 합니다").

합니다 *UpdateModel()* 모델 개체에서 속성에 양식 값을 할당 하는 동안 오류가 발생할 경우 도우미 메서드 ModelState 컬렉션을 자동으로 채웁니다. 예를 들어 EventDate 속성은 Dinner 개체의 날짜/시간 형식입니다. UpdateModel() 메서드 위의 시나리오에서 "BOGUS" 문자열 값을 할당할 수 없을 때 해당 속성을 사용 하 여 할당 오류를 나타내는 ModelState 컬렉션에 항목이 발생 UpdateModel() 메서드를 추가 합니다.

개발자는 "catch" 오류 처리 블록에서 현재 규칙 위반을 기준으로 항목을 사용 하 여 ModelState 컬렉션 채워지는 내에서 아래 수행 하는 것 처럼 ModelState 컬렉션에 오류 항목을 명시적으로 추가 하는 코드를 작성할 수도 합니다 저녁 식사 개체:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a>ModelState와 html 도우미 통합

HTML 도우미 메서드-Html.TextBox()-같은 출력을 렌더링할 때 ModelState 컬렉션을 확인 합니다. 항목에 대 한 오류가 있는 경우 사용자가 입력 한 값과 CSS 오류 클래스를 렌더링 합니다.

예를 들어, "편집" 보기에서는 사용 Html.TextBox() 도우미 메서드는 EventDate은 Dinner 개체의 렌더링:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

오류 시나리오에서 뷰를 렌더링 되 면 Html.TextBox() 메서드 ModelState 컬렉션은 Dinner 개체의 "EventDate" 속성과 관련 된 오류가 발생 한 경우 참조를 확인 합니다. 오류가 발생 하는 것이 판단 하는 경우 값으로 제출 된 사용자 입력 ("BOGUS")를 렌더링 하 고 css 오류 클래스를 추가 합니다 &lt;입력 형식 = "textbox" /&gt; 태그 생성:

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

하지만 원하는 검색할 css 오류 클래스의 모양을 사용자 지정할 수 있습니다. – "입력-유효성 검사 오류" – 기본 CSS 오류 클래스에 정의 되어는 *\content\site.css* 아래와 같은 스타일 시트와 같습니다.

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

이 CSS 규칙은 아래와 같은 강조 표시 하는 잘못 된 입력된 요소를 일으킨 원인을:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a>Html.ValidationMessage() 도우미 메서드

특정 모델 속성과 관련 된 오류 메시지가 출력 ModelState Html.ValidationMessage() 도우미 메서드를 사용할 수 있습니다.:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

위의 코드 출력:  *&lt;p a n class = "필드 유효성 검사 오류"&gt; 'BOGUS' 값이 올바르지 않습니다&lt;s&gt;*

Html.ValidationMessage() 도우미 메서드는 또한 개발자가 표시 되는 오류 텍스트 메시지를 재정의할 수 있도록 하는 두 번째 매개 변수를 지원 합니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

위의 코드 출력:  <em>&lt;p a n class = "필드 유효성 검사 오류"&gt;\*&lt;s&gt;</em>기본 오류 텍스트에 대 한 오류가 있으면 대신 합니다 EventDate 속성입니다.

##### <a name="htmlvalidationsummary-helper-method"></a>Html.ValidationSummary() 도우미 메서드

와 함께 요약 오류 메시지를 렌더링할 Html.ValidationSummary() 도우미 메서드를 사용할 수는 &lt;ul&gt;&lt;li /&gt;&lt;/u l&gt; 목록을 모두 자세한 오류 메시지는 ModelState 컬렉션:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

Html.ValidationSummary() 도우미 메서드를 사용 하는 자세한 오류 목록 위에 표시할 요약 오류 메시지를 정의 하는 선택적 문자열 매개-변수:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

필요에 따라 오류 목록 모양을 재정의 하려면 CSS를 사용할 수 있습니다.

#### <a name="using-a-addruleviolations-helper-method"></a>AddRuleViolations 도우미 메서드를 사용 하 여

해당 catch 블록 내에서 foreach 문을 Dinner 개체의 규칙 위반을 반복 하 여 컨트롤러의 ModelState 컬렉션에 추가 하는 데 사용 하는 초기 HTTP POST 편집 구현:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

에서는이 코드는 "ControllerHelpers"를 추가 하 여 거의 깔끔하고 NerdDinner 프로젝트에 클래스 및 도우미 메서드는 ASP.NET MVC ModelStateDictionary 클래스를 추가 하는 그 안에 "AddRuleViolations" 확장 메서드를 구현 가능 합니다. 이 확장 메서드 ModelStateDictionary RuleViolation 오류 목록을 채우는 데 필요한 논리를 캡슐화 할 수 있습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

그런 다음이 확장 메서드는 Dinner 규칙 위반을 사용 하 여 ModelState 컬렉션을 채우는 데 사용 하는 HTTP POST 편집 작업 메서드를 업데이트할 수 있습니다.

#### <a name="complete-edit-action-method-implementations"></a>편집 작업 메서드 구현은 완료

아래 코드의 모든 편집 시나리오에 필요한 컨트롤러 논리를 구현합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

편집 구현에 대 한 가지 좋은 점은 컨트롤러 클래스도 아니고 보기 템플릿은 Dinner 모델에 의해 적용 되는 비즈니스 규칙 또는 특정 유효성 검사에 대 한 모든 것을 알아야 했습니다. 모델에 추가 규칙 나중에 추가할 수 있습니다 하 고 컨트롤러 또는 보기에서 순서 대로 지원 하기 위해 코드 변경할 필요가 없습니다. 이 응용 프로그램의 요구 사항을 나중에 최소를 사용 하 여 코드 변경 내용 쉽게 발전 하는 유연 하 게 제공 합니다.

### <a name="create-support"></a>만들기 지원

구현 DinnersController 클래스의 "편집" 동작을 마쳤습니다. 보겠습니다 이제 이동할에 – 사용자가 새 Dinners에 추가할 수 있도록 해 주는 "만들기" 지원을 구현 합니다.

#### <a name="the-http-get-create-action-method"></a>HTTP GET 작업 메서드 만들기

HTTP "GET" 동작을 구현 하 여 먼저는 작업 메서드를 만듭니다. 사용자가 방문 하면이 메서드가 호출 됩니다 합니다 *Dinners/만들기* URL입니다. 구현은 다음과 같습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

위의 코드 새 Dinner 개체를 만들고 해당 EventDate 속성을 나중에 1 주일 수를 할당 합니다. 그런 다음 새 Dinner 개체를 기반으로 하는 뷰를 렌더링 합니다. 이름을 명시적으로 전달 하지 않았으므로 합니다 *View()* 도우미 메서드를 보기 템플릿은 해결 하려면 규칙 기반 기본 경로 사용 하면 해당: /Views/Dinners/Create.aspx 합니다.

이 보기 템플릿은 이제 만들어 보겠습니다. 만들기 작업 메서드 내에서 마우스 오른쪽 단추로 클릭 하 고 "추가 보기" 상황에 맞는 메뉴 명령을 선택 하 여이 작업을 수행 수입니다. "뷰 추가" 대화 상자 내에서 보기 템플릿에 Dinner 개체를 전달 하는 것 및 자동-스 캐 폴드를 "만들기" 템플릿을 선택 나타냅니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

"추가" 단추를 클릭 하는 경우 Visual Studio 새 스 캐 폴드 기반 "Create.aspx" 보기 "\Views\Dinners" 디렉터리에 저장 되며 IDE 내에서 열어 됩니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

보겠습니다 우리에 게 있어 기본 "만들기" 스 캐 폴드 파일 생성 된 몇 가지 변경 하 고 다음과 같이 표시를 수정:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

이제을 실행할 때이 응용 프로그램 및 액세스 하 고는 *"/ Dinners/만들기"* 만들기 작업 구현에서 아래와 같은 UI 렌더링 됩니다 브라우저 내에서 URL:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a>동작 메서드를 만드는 HTTP POST를 구현 합니다.

HTTP GET 메서드 버전을이 만들기 작업 구현 했습니다. 폼 post를 실행 하 고 "저장" 단추를 클릭할 때 수행 합니다 *Dinners/만들기* URL HTML 제출 &lt;입력&gt; HTTP POST 동사를 사용 하 여 값을 형성 합니다.

HTTP POST 동작을 이제 구현 해 보겠습니다 우리의 작업 메서드를 만듭니다. HTTP POST 시나리오 처리 여부를 나타내는 "AcceptVerbs" 특성에는 우리의 DinnersController 오버 로드 "만들기" 작업 메서드도 추가 시작 합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

다양 한 방법으로 게시 된 폼 매개 변수는 HTTP POST를 사용 하도록 설정 "만들기" 메서드 내에서 액세스할 수 있습니다.

한 가지 방법은 새 Dinner 개체를 만들고 사용 하 여 하는 *UpdateModel()* 도우미 메서드 (예: 수행한 편집 작업을 사용 하 여) 게시 된 양식 값으로 채웁니다. 우리의 DinnerRepository를 추가 하 고 데이터베이스에 유지 다음 아래 코드를 사용 하 여 새로 만든된 저녁을 표시 하는 세부 정보 작업에 사용자를 리디렉션한 다음 했습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

또는 메서드 매개 변수로 Dinner 개체를 사용 하는 create () 동작 메서드에 있는 접근 방식을 사용할 수 있습니다. ASP.NET MVC는 다음 자동으로 한 새 Dinner 개체를 인스턴스화, 양식 입력을 사용 하 여 해당 속성 채우고 우리의 작업 메서드에 전달:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

위의 작업 메서드는 Dinner 개체에 성공적으로 채워졌는지 폼 게시 값을 사용 하 여 ModelState.IsValid 속성을 확인 하 여 확인 합니다. 없으면 false 변환 문제 입력이 반환 됩니다 (예: EventDate 속성에 대 한 "BOGUS" 문자열), 문제가 있는 경우이 동작 메서드에 다시 표시 되 고 및 합니다.

입력된 값이 유효 하면 동작 메서드를 추가 하 고 새 저녁 식사를 DinnerRepository 저장을 시도 합니다. Try/catch 블록 내에서이 작업을 래핑하고 다시 표시 되는 경우 (유발 하는 예외를 발생 시키려면 dinnerRepository.Save() 메서드)는 비즈니스 규칙 위반 합니다.

이 오류 처리 동작의 동작을 확인 하려면 요청 수를 *Dinners/만들기* URL 및 새 저녁에 대 한 정보를 입력 합니다. 잘못 된 입력 또는 값에는 아래와 같은 강조 표시 하는 오류와 함께 다시 표시 하려면 폼 만들기 하면 합니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

만들기 폼 정확히 동일한 유효성 검사 및 비즈니스 규칙을 편집 양식에 인식 하는 방법을 확인할 수 있습니다. 이 유효성 검사 및 비즈니스 모델에 정의 된 규칙과 UI 또는 응용 프로그램의 컨트롤러 내에서 포함 되지 때문입니다. 즉, 있습니다 나중에 변경/발전시키는 유효성 검사 또는 비즈니스 규칙에서 단일 배치 하 고 응용 프로그램 전체에서 적용 합니다. 우리는 필요가 없습니다 내에서 모든 코드는 편집 변경 또는 새 규칙이 나 기존 수정 사항이 자동으로 적용 하도록 동작 메서드를 만듭니다.

입력된 값을 수정 하 고 "저장" 단추를 클릭 합니다 DinnerRepository에는 추가 성공 하 고 데이터베이스에 추가할 새 Dinner 다시 합니다. 에서는 다음 리디렉션됩니다 합니다 */Dinners 세부 정보 / [id]* URL – 새로 만든된 저녁에 대 한 정보를 사용 하 여 우리가 표시 하는 위치:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a>Delete 지원

우리의 DinnersController에 "삭제" 지원을 지금 추가 하겠습니다.

#### <a name="the-http-get-delete-action-method"></a>HTTP GET Delete 동작 메서드

Delete 동작 메서드는 HTTP GET 동작을 구현 하 여 시작 됩니다. 사용자가 방문 하면이 메서드가 호출 됩니다 합니다 */Dinners/삭제 / [id]* URL입니다. 다음은 구현이입니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

작업 메서드는 삭제할 저녁 식사를 검색 하려고 합니다. Dinner 있는 렌더링 하는 경우 뷰 개체를 기준으로 Dinner 합니다. 개체 (없거나 이미 삭제 된) 해당 하는 경우 "NotFound"를 렌더링 하는 뷰를 반환 우리의 "Details" 동작 메서드에 대 한 이전에 만든 서식 파일을 보려면.

Delete 동작 메서드 내에서 마우스 오른쪽 단추로 클릭 하 고 "추가 보기" 상황에 맞는 메뉴 명령을 선택 하 여 "삭제" 보기 템플릿을 만들 수 있습니다. "뷰 추가" 대화 상자 내 보기 템플릿은 해당 모델로 Dinner 개체를 전달 하는 것 및 빈 템플릿을 만들려는 나타냅니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

"추가" 단추를 클릭 하는 경우 Visual Studio는이 "\Views\Dinners" 디렉터리 내에서 새 "Delete.aspx" 보기 템플릿 파일을를에 추가 합니다. 일부 HTML 및 코드 삭제 확인 화면이 구현 하려면 템플릿에 추가 아래와 같은:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

위의 코드는 삭제할 Dinner 및 출력의 제목을 표시를 &lt;폼&gt; 최종 사용자가 그 안에 "삭제" 단추를 클릭 하면 /Dinners/삭제 / [id] URL에 POST를 수행 하는 요소입니다.

액세스 회원과 응용 프로그램을 실행할 때 합니다 *"/ Dinners/삭제 / [id]"* 유효한 저녁에 대 한 URL 개체 아래와 같은 UI 렌더링:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| **쪽 항목: 우리가 왜 게시물?** |
| --- |
| 궁금할 – 이유는 무엇 일까요의 노력을 통해는 &lt;폼&gt; 우리의 삭제 확인 화면 내에서? 실제 삭제 작업을 수행 하는 동작 메서드에 연결 표준 하이퍼링크를 방금 사용 하지 않는 이유는? 이유는 웹 크롤러에 대비 하 고 검색 엔진 Url을 검색 하 고 링크를 따릅니까 때 삭제할 데이터를 실수로 인해 주의 때문입니다. HTTP GET 기반 Url 액세스/탐색 하기 위해 "안전한" 것으로 간주 됩니다 및 HTTP-POST 작업을 수행 하지 할 됩니다. 항상 안전 하지 않은 배치 또는 HTTP POST 요청 뒤 데이터 수정 작업 해야 하는 것이 좋습니다. |

#### <a name="implementing-the-http-post-delete-action-method"></a>HTTP POST Delete 동작 메서드를 구현합니다.

이제 삭제 확인 화면이 표시 하는 구현 하는 Delete 동작 메서드의 GET HTTP 버전입니다. 최종 사용자가 "삭제" 단추를 클릭 하면 폼 post를 수행 합니다 */Dinners Dinner / [id]* URL입니다.

아래 코드를 사용 하 여 삭제 작업 메서드의 HTTP "POST" 동작을 이제 구현 해 보겠습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

Delete 동작 메서드는 HTTP POST 버전이 삭제 하려면 dinner 개체를 검색 하려고 시도 합니다. (이미 삭제 된) 때문이 찾을 수 없는 경우 "NotFound" 템플릿은 렌더링 합니다. Dinner를 찾으면는 DinnerRepository에서 삭제 합니다. "삭제" 템플릿을 렌더링합니다.

"삭제" 템플릿을 구현 하에서는 작업 메서드에서 마우스 오른쪽 단추로 클릭 하 고 "추가 보기" 상황에 맞는 메뉴를 선택 합니다. "삭제" 보기 이름을 하 고 빈 템플릿을 수 (및 강력한 형식의 모델 개체를 사용 하지) 하 게 됩니다. 일부 HTML 콘텐츠를 추가 하겠습니다 했습니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

이제을 실행할 때이 응용 프로그램 및 액세스 하 고는 *"/ Dinners/삭제 / [id]"* 우리의 저녁 렌더링할 개체 삭제 확인 하는 유효한 저녁 URL 아래와 같은 화면:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

"삭제" 단추를 클릭 하는 경우에 HTTP POST를 수행 합니다 */Dinners/삭제 / [id]* Dinner에서는 데이터베이스에서 삭제 하 고 "삭제" 보기 템플릿은 표시 URL:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a>모델 바인딩 보안

ASP.NET MVC의 기본 모델 바인딩 기능을 사용 하는 두 가지에 설명 했습니다. 먼저 UpdateModel() 메서드를 사용 하 여 기존 모델 개체에 속성을 업데이트 하 고 사용 하 여 두 번째 모델 개체의 동작 메서드 매개 변수로 전달 하는 것에 대 한 ASP.NET MVC의 지원 합니다. 이러한 기술은 모두 매우 강력 하 고 매우 유용 합니다.

이 power 하면 책임입니다. 것은 항상 보안에 대 한 편집 광 사용자 입력을 수락 하는 경우에 마찬가지 양식 입력 개체에 바인딩할 때 하며 에 주의 해야 항상 HTML 인코딩 HTML 및 JavaScript 주입 공격을 방지 하 고 SQL 주입 공격에 주의 해야 사용자가 입력 한 값 (참고:이 응용 프로그램을 자동으로이 방지 하기 위해 매개 변수를 인코딩하는 방법에 대 한 LINQ to SQL 사용 공격 형식)입니다. 되지 단독으로 클라이언트 쪽 유효성 검사에 의존 하 고 항상 해커 위조 값을 보내려는 시도 방지 하기 위해 서버 쪽 유효성 검사를 사용 해야 합니다.

ASP.NET MVC의 바인딩 기능을 사용 하는 경우에 대해 생각해 야 되도록 한 추가 보안 항목에 바인딩하는 개체의 범위입니다. 특히 허용 바인딩될 실제로 업데이트할 최종 사용자가 업데이트할 수 있는 해야 하는 속성만 허용 되는지 확인 하는 속성의 보안 의미를 파악 하려고 합니다.

기본적으로 UpdateModel() 메서드는 들어오는 형식 매개 변수 값과 일치 하는 모델 개체에서 모든 속성을 업데이트 하려고 합니다. 마찬가지로, 기본적으로도 작업 메서드 매개 변수로 전달 된 개체 형식 매개 변수를 통해 설정 하는 해당 속성을 모두 가질 수 있습니다.

#### <a name="locking-down-binding-on-a-per-usage-basis"></a>사용 당 기준 바인딩 잠금

제공 하는 명시적 "include 목록" 업데이트할 수 있는 속성의 바인딩 정책 사용 당 단위로 제한할 수 있습니다. 이 아래와 같은 UpdateModel() 메서드에 추가 하는 문자열 배열 매개 변수에 전달 하 여 수행할 수 있습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

또한 작업 메서드 매개 변수로 전달 된 개체는 "include 목록"의 속성을 아래와 같은 지정을 사용할 수 있도록 [바인딩] 특성을 지원 합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a>바인딩 형식으로 잠그지

형식당 하나의 단위로 바인딩 규칙을 제한할 수도 있습니다. 따라서 모든 컨트롤러 및 작업 메서드 (UpdateModel와 작업 메서드 매개 변수 시나리오 포함)는 모든 시나리오에 적용할 수 있도록 및 바인딩 규칙을 한 번만 지정할 수 있습니다.

형식으로 [바인딩] 특성을 추가 하거나 (형식이 없고 시나리오에 유용) 응용 프로그램의 Global.asax 파일 내에서 등록 하 여 형식당 하나의 바인딩 규칙을 사용자 지정할 수 있습니다. 바인딩 특성의 포함을 사용할 수 있습니다. 제외 되는 속성을 제어 하는 속성은 특정 클래스 또는 인터페이스에 대 한 바인딩 가능한 하며

NerdDinner 응용 프로그램에서는 Dinner 클래스에 대 한이 기술을 사용 하 고 다음 바인딩 가능한 속성의 목록을 제한 하 고 [바인딩] 특성을 추가할 것:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

바인딩을 통해 조작할 않으십니까 컬렉션을 허용 하지 않는 것을 확인 하거나 바인딩을 통해 설정할 DinnerID 또는 HostedBy 속성을 허용 했습니다. 보안상의 이유로에서는에서는 대신만 조작 작업 메서드 내에서 명시적 코드를 사용 하 여 이러한 특정 속성입니다.

### <a name="crud-wrap-up"></a>CRUD 요약

ASP.NET MVC에는 다양 한 시나리오를 게시 하는 폼 구현에 도움이 되는 기본 제공 기능이 포함 되어 있습니다. 우리의 DinnerRepository 위에 CRUD UI를 지원 하려면 다양 한 이러한 기능을 사용 했습니다.

응용 프로그램을 구현 하는 모델 중심 접근 방법을 사용 합니다. 즉, 모든 유효성 검사 및 비즈니스 규칙 논리는 컨트롤러 또는 뷰를 그리고 우리의 모델 계층 – 내에서 정의 됩니다. 컨트롤러 클래스도 아니고 우리의 보기 템플릿은 Dinner 모델 클래스에 의해 적용 되는 특정 비즈니스 규칙에 대해 알 합니다.

응용 프로그램 아키텍처를 정리 유지 되 고 쉽게 테스트 됩니다. 이 모델 계층에 비즈니스 규칙을 추가로 나중에 추가할 수 있습니다 및 *코드를 변경 하지 않아도* 컨트롤러 또는 보기에서 해당 순서 대로 지원 됩니다. 상당한 발전 하 고 나중에 응용 프로그램을 변경 하는 민첩성을 제공 하는 것이입니다.

우리의 DinnersController 이제 Dinner 목록/세부 정보를 사용 하도록 설정 뿐만 아니라 만들기, 편집 및 삭제 지원입니다. 아래 클래스에 대 한 전체 코드를 찾을 수 있습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a>다음 단계

이제 DinnersController 클래스 내에서 구현 하는 기본 CRUD (만들기, 읽기, 업데이트 및 삭제) 지원 합니다.

이제 살펴보겠습니다 사용 하 여 ViewData 및 ViewModel 클래스는 폼에 풍부한 UI를 사용 하도록 설정 합니다.

> [!div class="step-by-step"]
> [이전](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [다음](use-viewdata-and-implement-viewmodel-classes.md)
