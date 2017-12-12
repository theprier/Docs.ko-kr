---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: "제공 CRUD (만들기, 읽기, 업데이트, 삭제) 데이터 항목 지원 구성 | Microsoft Docs"
author: microsoft
description: "5 단계 편집, 만들고도 함께 Dinners 삭제에 대 한 지원 활성화 여 DinnersController 클래스 추가 하는 방법을 보여 줍니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: 5a314a1761527d8a2273166a743e3deac012a557
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="provide-crud-create-read-update-delete-data-form-entry-support"></a>제공 CRUD (만들기, 읽기, 업데이트, 삭제) 데이터 항목 지원 구성
====================
여 [Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 5 단계로 ["업그레이드 되었으며 수정" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 하는 워크 쓰루는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 5 단계 편집, 만들고도 함께 Dinners 삭제에 대 한 지원 활성화 여 DinnersController 클래스 추가 하는 방법을 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a>업그레이드 되었으며 수정 5 단계: 만들기, 업데이트 및 삭제 양식 시나리오

고 했으므로 이러한 내용을 컨트롤러와 뷰를 도입 하는 사이트에 Dinners에 대 한 목록/세부 정보 환경을 구현 하는 데 사용 하는 방법을 설명 합니다. 다음 단계를 추가로 DinnersController 클래스를 가져간 편집, 만들고도 함께 Dinners 삭제에 대 한 지원을 사용 하도록 설정 됩니다.

### <a name="urls-handled-by-dinnerscontroller"></a>DinnersController에서 처리 하는 Url

두 Url에 대 한 지원을 구현 DinnersController에 작업 메서드 이전에 추가한: */Dinners* 및 */Dinners/세부 정보 / [id]*합니다.

| **URL** | **동사** | **용도** |
| --- | --- | --- |
| */Dinners/* | 가져오기 | 예정 된 dinners 목록이 있는 HTML을 표시 합니다. |
| */Dinners/세부 정보 / [id]* | 가져오기 | 특정 저녁에 대 한 세부 정보를 표시 합니다. |

이제 세 개의 추가 Url을 구현 하는 작업 메서드 추가 합니다: */Dinners/편집 / [id], / Dinners/만들기,*및*/Dinners/Delete / [id]*합니다. 이러한 Url 편집 기존 Dinners 새 Dinners을 만들고 Dinners 삭제 지원 하도록 설정 됩니다.

HTTP GET 및 HTTP POST 동사와의 상호 작용 새 Url이 지원 됩니다. 이러한 Url에 HTTP GET 요청 ("edit"의 경우 Dinner 데이터 입력 폼, "만들기"의 경우 새 양식 및 삭제 확인 화면이 "삭제"의 경우) 데이터의 초기 한 HTML 뷰가 표시 됩니다. 이러한 Url HTTP POST 요청 우리의 DinnerRepository (및 데이터베이스에는 여기에서) Dinner 데이터를 저장/업데이트/삭제 됩니다.

| **URL** | **동사** | **용도** |
| --- | --- | --- |
| */Dinners/편집 / [id]* | 가져오기 | 저녁 데이터로 채워진 편집 가능한 HTML 폼을 표시 합니다. |
| 올리기 | 데이터베이스에 특정 저녁에 폼 변경 내용을 저장 합니다. |
| */ Dinners/만들기* | 가져오기 | 사용자가 새 Dinners 정의할 수 있는 빈 HTML 폼을 표시 합니다. |
| 올리기 | 새 Dinner 만들고 데이터베이스에 저장 합니다. |
| */Dinners/delete / [id]* | 가져오기 | 삭제 확인 화면을 표시 합니다. |
| 올리기 | 데이터베이스에서 지정 된 dinner를 삭제합니다. |

### <a name="edit-support"></a>편집 지원

"Edit" 시나리오를 구현 하 여 시작 해 보겠습니다.

#### <a name="the-http-get-edit-action-method"></a>HTTP GET 편집 동작 메서드

이 편집 동작 메서드의 HTTP "GET" 동작을 구현 하 여 시작 합니다. 이 메서드가 됩니다 될 때 호출 되는 */Dinners/편집 / [id]* URL을 요청 합니다. 구현은 같이 표시 됩니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

위의 코드는 DinnerRepository를 사용 하 여 Dinner 개체를 검색 합니다. 그러면 Dinner 개체를 사용 하 여 보기 서식 파일을 렌더링 합니다. 서식 파일 이름을 명시적으로 전달 하지 않은 것 이므로 *View()* 도우미 메서드를 템플릿 보기를 해결 하려면 규칙 기반 기본 경로 사용 합니다: /Views/Dinners/Edit.aspx 합니다.

이제이 뷰 서식 파일을 만들어 보겠습니다. Edit 메서드 내에서 마우스 오른쪽 단추로 클릭 하 고 "뷰 추가" 상황에 맞는 메뉴 명령 선택 하 여 수행 됩니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

"뷰 추가" 대화 상자 내에서 우리 합니다 나타내고 म 해당 모델로 템플릿 우리의 보기를 Dinner 개체를 전달 하는 자동 스 캐 폴드를 "편집" 템플릿을 선택:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

"추가" 단추를 클릭 하면 Visual Studio는 "\Views\Dinners" 디렉터리 내에서 "Edit.aspx" 보기 템플릿 파일을 새를 us에 대 한 추가 합니다. 또한 편집기-코드 – "편집" 스 캐 폴드 구현이 초기 같은 아래 채워진 내에서 새 "Edit.aspx" 보기 서식 파일을는 것이 열립니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

보겠습니다 기본 "편집" scaffold 생성에 대 한 몇 가지 변경 하 고 편집 보기 템플릿 (노출 않으려는 속성 중 일부를 제거) 하는 콘텐츠의 아래을 업데이트 합니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

응용 프로그램 및 요청을 실행할 때의 *"/ 1/편집/Dinners"* URL 페이지를 살펴봅니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

이 보기에 의해 생성 된 HTML 태그 아래와 같습니다. 표준 HTML –는 &lt;양식&gt; HTTP POST를 수행 하는 요소는 */Dinners/Edit/1* URL 때 "저장" &lt;입력 형식 = "제출" /&gt; 단추를 누르면 합니다. HTML &lt;type = "text" /&gt; 요소는 편집 가능한 각 속성에 대 한 출력 되었습니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a>Html.BeginForm() 및 Html.TextBox() Html 도우미 메서드

템플릿 우리의 "Edit.aspx" 보기는 몇 가지 방법 "Html 도우미": Html.ValidationSummary(), Html.BeginForm(), Html.TextBox(), 및 Html.ValidationMessage() 합니다. Us에 대 한 HTML 태그를 생성, 외에도 이러한 도우미 메서드 제공 기본 제공 오류 처리 및 유효성 검사를 지원 합니다.

##### <a name="htmlbeginform-helper-method"></a>Html.BeginForm() 도우미 메서드

Html.BeginForm() 도우미 메서드는 HTML 출력 &lt;양식&gt; 우리의 태그 요소에에서 있습니다. 우리의 Edit.aspx 뷰 템플릿에 적용 중인 C# "using" 문을이 방법을 사용할 경우 알 수 있습니다. 왼쪽 중괄호의 시작을 나타냅니다는 &lt;양식&gt; 의 끝을 나타내는 작업은 콘텐츠 및 닫는 중괄호는 &lt;/f&gt; 요소:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

또는 "using" 문을 찾을 경우 다음과 같은 시나리오에 부자연 스러운 접근, Html.BeginForm() 및 Html.EndForm() 조합으로 서 (같은 작업을 수행)을 사용할 수 있습니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

Html.BeginForm() 매개 변수 없이 호출 하면 현재 요청 URL에 HTTP POST를 수행 하는 폼 요소를 출력 합니다. 이 편집 보기 생성 이유 즉는  *&lt;양식 동작 = "/ 1/편집/Dinners" 메서드 "post" =&gt;*  요소입니다. म 수 또는 조건이 충족 명시적 매개 변수 Html.BeginForm()를 다른 URL에 게시 하 려 하는 경우.

##### <a name="htmltextbox-helper-method"></a>Html.TextBox() 도우미 메서드

Edit.aspx 시각 Html.TextBox() 도우미 메서드를 사용 하 여 출력에 &lt;type = "text" /&gt; 요소:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

id/이름 특성을 지정 하는 데 사용 되는 단일 매개 변수-를 사용 하는 위의 Html.TextBox() 메서드는 &lt;type = "text" /&gt; 으로 출력에서 textbox 값을 채우기 위해 모델 속성에는 요소입니다. 예를 들어 편집 뷰에 전달에서는 Dinner 개체 ".NET 미래", "Title" 속성 값을 가지 며 없으므로 우리의 Html.TextBox("Title") 메서드 호출 출력:  *&lt;입력된 id = "제목" name = "제목" type = "text" value = ".NET 미래" /&gt;* .

또는 사용 하 여 첫 번째 Html.TextBox() 매개 변수는 요소의 id/이름을 지정 하 고 두 번째 매개 변수로 사용할 값에 명시적으로 전달:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

종종 출력 값에 사용자 지정 형식 지정을 수행 해야 합니다. .NET에 기본 제공 string.format () 정적 메서드는 이러한 시나리오에 유용 합니다. 우리의 Edit.aspx 보기 템플릿 시간을 초를 표시 되지 않습니다 (이 DateTime 형식) EventDate 값의 서식을 지정 하려면이 사용 됩니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

필요에 따라 Html.TextBox() 세 번째 매개 변수 추가 HTML 특성을 출력 데 사용할 수 있습니다. 코드 조각 아래 추가 크기를 렌더링 하는 방법을 보여 줍니다 = "30" 특성과 클래스 = "mycssclass" 특성에는 &lt;type = "text" /&gt; 요소입니다. 방법을 사용 하 여 클래스 특성의 이름을 이스케이프는 것을 참고는 "@" character because "클래스"는 C#의 예약 된 키워드.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a>HTTP POST 편집 동작 메서드를 구현합니다.

구현 하는 편집 작업 메서드의 HTTP GET 버전을 사용할 수 있습니다. 사용자가 요청 하는 경우는 */Dinners/Edit/1* 다음과 같이 HTML 페이지를 수신 하는 URL:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

폼 post를 사용 하면 "저장" 버튼을 눌러서는 */Dinners/Edit/1* URL, HTML 전송 &lt;입력&gt; HTTP POST 동사를 사용 하 여 값을 형성 합니다. 저장 하는 Dinner 처리할 우리의 편집 동작 메서드에 –의 HTTP POST 동작을 이제 구현 해 보겠습니다.

HTTP POST 시나리오를 처리 하는 것을 나타내는 "AcceptVerbs" 특성에 우리의 DinnersController를 오버 로드 된 "편집" 동작 메서드를 추가 하 여 시작 합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

오버 로드 된 작업 메서드에 [AcceptVerbs] 특성이 적용 되 면 ASP.NET MVC는 자동으로 들어오는 HTTP 동사에 따라 적절 한 동작 메서드에 디스패치 요청을 처리 합니다. HTTP POST 요청을 */Dinners/편집 / [id]* Url이 다른 모든 HTTP 동사 요청을 하는 동안 위의 Edit 메서드를 이동 합니다 */Dinners/편집 / [id]*Url은 이동 하는 첫 번째 편집 메서드를 구현 했습니다 (않은 있음 한 [AcceptVerbs] 특성).

| **HTTP 동사를 통해 쪽 주제: 이유 구분?** |
| --- |
| 궁금할 것 – 단일 URL을 사용 하 고 HTTP 동사를 통해는 동작을 차별화는? 편집 저장 하 고 로드를 처리 하는 두 개의 별도 Url만 하면 안 되나요? 예를 들어: /Dinners/편집 / [id] 및 표시 하는 초기 폼 /Dinners/저장 / [id] 저장 하는 폼 게시를 처리 하 시겠습니까? 두 개의 별도 Url을 게시 단점은 /Dinners/Save/2에 게시 한 HTML 폼 입력된 오류로 인해 다시 표시 해야 했습니다을 경우 최종 사용자 (이후에 브라우저의 주소 표시줄에 Dinners/저장/2 URL으로 종료 됩니다. URL에 게시 되는 폼)입니다. 최종 사용자가 브라우저 즐겨찾기 목록에이 redisplayed 페이지 책갈피를 설정 하거나 URL 복사/붙여 넣습니다. 및 친구에 게 전자 메일로 하는 경우 (URL을 게시 값에 따라 다름) 이후 나중에 작동 하지 않는 URL 저장 결국 것입니다. 단일 URL을 노출 하 여 (같은: /Dinners/Edit/[id]) 및 HTTP 동사는 처리를 구분 하는 방식 것이 안전 하 게 보호 하는 최종 사용자를 편집 페이지를 책갈피 및/또는 다른 사용자에 게 URL을 보냅니다. |

#### <a name="retrieving-form-post-values"></a>폼 게시 값 검색

다양 한 폼 매개 변수는 HTTP POST "편집" 메서드 내에서 게시 방법 액세스할 수 있습니다. 한 가지 간단한 방법은 방금 폼 컬렉션에 액세스 하 여 게시 된 값을 직접 검색 컨트롤러 기본 클래스에서 요청 속성을 사용 하는 것입니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

오류 처리 논리를 추가 되 면 특히는 위의 방법 하지만 약간 자세한 정보입니다.

이 시나리오는 기본 제공을 활용 하는 방식이 더 효과적 *UpdateModel()* 컨트롤러 기본 클래스 도우미 메서드입니다. 들어오는 폼 매개 변수를 사용 하 여 전달 하는 개체의 속성을 업데이트를 지원 합니다. 리플렉션을 사용 하 여 개체에 속성 이름을 결정 하 고 자동으로 변환 하 고 클라이언트에서 전송한 입력된 값에 따라에 값을 할당 합니다.

이 코드를 사용 하 여 우리의 HTTP POST 편집 작업을 간소화 하기 위해 UpdateModel() 메서드를 사용할 수 있습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

방문 이제 우리는 */Dinners/Edit/1* URL 및 우리의 Dinner의 제목 변경 합니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

"저장" 단추를 클릭 폼 게시 우리의 편집 작업을 수행 하겠습니다 및 업데이트 된 값을 데이터베이스에 유지 됩니다. 그런 다음 리디렉션됩니다 세부 정보 URL로 (있음 새로 저장 된 값이 표시 됩니다) 저녁에:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a>편집 오류 처리

경우는 제외 우리의 현재 HTTP POST 구현 works 미세 – 오류가 있습니다.

사용자가 양식 편집 실수 때 해결 하도록 안내 하는 자세한 오류 메시지와 함께 폼이 다시 표시 되도록 해야 합니다. 여기에 최종 사용자가 입력이 잘못 되었습니다를 게시 하는 경우 (예: 잘못 된 형식의 날짜 문자열) 인 사례 한 입력 형식이 올바르지 않은 비즈니스 규칙 위반 처럼 합니다. 오류가 발생 한 경우 양식을 처음 변경 내용을 수동으로 다시 부여 되지 않도록 입력 한 사용자 입력된 데이터를 보존 해야 합니다. 이 프로세스는 폼 성공적으로 완료 될 때까지 필요한 만큼 여러 번 반복 해야 합니다.

ASP.NET MVC에는 오류 처리 및 양식 다시 쉽게 하는 몇 가지 유용한 기본 제공 기능이 포함 되어 있습니다. 작업에서 이러한 기능을 보겠습니다 보려면 우리의 편집 동작 메서드를 다음 코드로 업데이트:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

위의 코드는 작업 주변 오류 처리 try/catch 블록에 배치 우리는 한다는 점을 제외 하면 이전 구현은 –와 비슷합니다. 예외가 발생 하면 UpdateModel()를 호출 하는 경우 또는 시도 하 고 (있음 Dinner 개체 저장 하려고 하 고 유효 하지 않을 경우이 모델 내에서 규칙 위반으로 인해 예외가 발생 하므로) DinnerRepository, 저장 하는 경우 catch 오류 처리 블록 우리의 됩니다. 실행 합니다. 저녁 개체에 있는 모든 규칙 위반을 반복에서는 내 (아래에서는 곧) 있는 ModelState 개체에 추가 합니다. 보기 다음 다시 표시합니다.

이 확인 하려면 보겠습니다 응용 프로그램을 다시 실행 작업 하는 Dinner 편집한 "BOGUS"의 EventDate 빈 제목을 있고 미국 국가 값을 가진 영국 전화 번호를 사용 하도록 변경 합니다. 우리의 HTTP POST 편집 메서드 (오류가 있기 때문에) Dinner 저장 할 수 있습니다 "저장" 단추를 누르면 하 고 양식을 다시 표시 됩니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

응용 프로그램 괜찮은 오류 경험을 있습니다. 잘못 된 입력이 포함 된 텍스트 요소 빨간색으로 강조 표시 됩니다 및 유효성 검사 오류 메시지에 대 한 최종 사용자에 게 표시 됩니다. 폼 원래 입력 한 사용자-입력된 데이터가 유지도 아무 것도 다시 부여 되지 않도록 합니다.

방법 인지 궁금할이 발생 했습니까? 어떻게 않은 EventDate, 제목과 ContactPhone 입력란 자체 빨간색으로 강조 표시 하 고 원래 입력 한 사용자 값을 출력 하도록 알고? 및 어떻게 않았습니다 오류 메시지 표시 맨 위에 있는 목록에? 다행히가 자동으로 발생 하지 않고가 기본 제공 쉽게 하는 입력된 유효성 검사 및 오류 처리 시나리오 ASP.NET MVC 기능의 일부만 사용 하기 때문에.

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a>ModelState 이해 및 유효성 검사 HTML 도우미 메서드

컨트롤러 클래스 뷰에 전달 되는 모델 개체에 오류가 있는지를 표시 하는 방법을 제공 하는 "ModelState" 속성 컬렉션을 가집니다. ModelState 컬렉션 내에서 오류 항목 문제가 있는 모델 속성의 이름을 식별 (예를 들어: "제목", "EventDate" 또는 "ContactPhone"), 사용자에 게 친숙 한 오류 메시지를 지정할 수 있도록 (예: "제목을 입력 해야 합니다.").

*UpdateModel()* 개체의 속성은 모델에 폼 값을 할당 하는 동안 오류가 발생 하는 경우 도우미 메서드 ModelState 컬렉션을 자동으로 채웁니다. 예를 들어 EventDate 속성 우리의 Dinner 개체의 날짜/시간 형식입니다. UpdateModel() 메서드 위의 시나리오에서 문자열 값 "BOGUS" 변수에 할당할 수 없을 때 할당 오류를 나타내는 ModelState 컬렉션에 항목을 해당 속성과 발생 UpdateModel() 메서드 추가.

개발자가 명시적으로 블록 내에서 당사의 "catch" 오류 처리 ModelState 컬렉션 항목에서 활성 규칙 위반을 기반으로 채워지는 아래 수행 하는 것 처럼 ModelState 컬렉션에 오류 항목을 추가 하는 코드를 작성할 수도 Dinner 개체:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a>ModelState와 html 도우미 통합

HTML 도우미 메서드-Html.TextBox()-같은 출력을 렌더링 하는 경우 ModelState 컬렉션을 검사 합니다. 항목에 대 한 오류가 있는 경우 사용자가 입력 한 값과 CSS 오류 클래스 렌더링 합니다.

예를 들어, "편집" 보기를 사용 하 여 사용 하 여 Html.TextBox() 도우미 메서드를 사용 하는 Dinner 개체의 EventDate 렌더링 하:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

뷰가 오류 시나리오에서 렌더링 된 Html.TextBox() 메서드 ModelState 컬렉션을 된 Dinner 개체의 "EventDate" 속성과 관련 된 오류가 있는지 참조를 확인 합니다. 것으로 확인 오류가 발생 했습니다 제출 된 사용자 입력 ("BOGUS")의 값으로 렌더링 되며 css 오류 클래스를 추가 &lt;type = "textbox" /&gt; 생성 된 태그:

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

그러나 해도 조회 하는 css 오류 클래스의 모양을 사용자 지정할 수 있습니다. – "입력-유효성 검사 오류" – 기본 CSS 오류 클래스에 정의 된는 *\content\site.css* 아래와 같은 스타일 시트와 같습니다.

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

이 CSS 규칙은 발생 한 이유를 아래와 같은 강조 표시는 잘못 된 입력된 요소입니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a>Html.ValidationMessage() 도우미 메서드

특정 모델 속성에 연결 된 ModelState 오류 메시지를 출력 Html.ValidationMessage() 도우미 메서드를 사용할 수 있습니다.:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

위의 코드를 출력:  *&lt;/><span class = "필드 유효성 검사 오류"&gt; 'BOGUS' 값이 잘못 &lt; /s&gt;*

또한 Html.ValidationMessage() 도우미 메서드는 개발자가 표시 되는 오류 텍스트 메시지를 재정의할 수 있도록 하는 두 번째 매개 변수를 지원 합니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

위의 코드를 출력:  *&lt;/><span class = "필드 유효성 검사 오류"&gt;\*&lt;/s&gt;*기본 오류 텍스트에 대 한 오류가 있으면 대신는 EventDate 속성입니다.

##### <a name="htmlvalidationsummary-helper-method"></a>Html.ValidationSummary() 도우미 메서드

와 함께 요약 오류 메시지를 렌더링 하 Html.ValidationSummary() 도우미 메서드를 사용할 수는 &lt;ul&gt;&lt;li /&gt;&lt;/ul&gt; 의 목록은 모든 자세한 오류 메시지는 ModelState 컬렉션:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

자세한 오류 목록 위에 표시할 요약 오류 메시지를 정의 하는 선택적 문자열 매개 변수-를 사용 하는 Html.ValidationSummary() 도우미 메서드입니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

필요에 따라 오류 목록 모양을 재정의에 CSS를 사용할 수 있습니다.

#### <a name="using-a-addruleviolations-helper-method"></a>AddRuleViolations 도우미 메서드를 사용 하 여

해당 catch 블록 내에서 foreach 문을 Dinner 개체의 규칙 위반을 반복 하 고 컨트롤러의 ModelState 컬렉션에 추가 하는 데 사용 하는 초기 HTTP POST 편집 구현:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

이 코드를 거의 깔끔하고 "ControllerHelpers"를 추가 하 여 업그레이드 되었으며 수정 프로젝트에 클래스 및 ASP.NET MVC ModelStateDictionary 클래스에는 도우미 메서드를 추가 하는 그 안에 "AddRuleViolations" 확장 메서드를 구현 하도록 수 있습니다. 이 확장 메서드 RuleViolation 오류 목록이 있는 ModelStateDictionary를 채우는 데 필요한 논리를 캡슐화 할 수 있습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

ModelState 컬렉션 우리의 Dinner 규칙 위반을이 확장 메서드를 사용 하 여 HTTP POST Edit 동작 메서드를 업데이트할 수 있습니다.

#### <a name="complete-edit-action-method-implementations"></a>편집 동작 메서드 구현은 완료

아래 코드의 모든 편집이 시나리오에 필요한 컨트롤러 논리를 구현합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

편집 구현에 대 한 점 해야 한다는 것 컨트롤러 클래스도 아니고 우리의 보기 템플릿 특정 유효성 검사 또는 예제의 Dinner 모델에 의해 강제 적용 하는 비즈니스 규칙에 대 한 어떠한 정보도 알 수 있습니다. 이 모델에 추가 규칙 나중에 추가할 수 하 고 우리의 컨트롤러 또는 지원 되는 데 대 한 보기를 코드 변경 필요가 없습니다. 응용 프로그램 요구 사항은 나중에 최소의 코드 변경 내용 쉽게 변경 하는 유연성과 제공 합니다.

### <a name="create-support"></a>만들기 지원

DinnersController 클래스의 "Edit" 동작을 구현 하는 작업을 완료 했습니다. 이제를 살펴보겠습니다에 – 사용자가을 새 Dinners를 추가할 수 있도록 설정 "만들기" 지원을 구현 합니다.

#### <a name="the-http-get-create-action-method"></a>HTTP GET 작업 메서드 만들기

HTTP "GET" 동작을 구현 하 여 먼저 우리의 동작 메서드를 만듭니다. 다른 사용자가 방문 하면이 메서드는 호출 된 */Dinners/만들기* URL입니다. 구현은 다음과 같습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

위의 코드에서 새 Dinner 개체를 만들고 해당 EventDate 속성을 나중에 1 주일 수를 할당 합니다. 그런 다음 새 Dinner 개체를 기반으로 하는 뷰를 렌더링 합니다. 하는 이름을 명시적으로 전달 하지 않은 것 이므로 *View()* 도우미 메서드를 템플릿 보기를 해결 하려면 규칙 기반 기본 경로 사용 합니다: /Views/Dinners/Create.aspx 합니다.

이제이 뷰 서식 파일을 만들어 보겠습니다. Create 작업 메서드 내에서 마우스 오른쪽 단추로 클릭 하 고 "뷰 추가" 상황에 맞는 메뉴 명령 선택 하 여 하겠습니다. "뷰 추가" 대화 상자 내에서 우리 합니다 나타내고 म 보기 템플릿에 Dinner 개체를 전달 하는 템플릿을 선택 하십시오. 자동-스 캐 폴드 하려면 "만들기":

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

"추가" 단추를 클릭 하면 Visual Studio "\Views\Dinners" 디렉터리에 새 스 캐 폴드 기반 "Create.aspx" 뷰를 저장 되 고 개방 IDE 내에서:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

Us에 대 한 기본 "만들기" 스 캐 폴드 파일에 생성 된 몇 가지 변경을 수행 하 고 아래 다음과 같이 표시를 수정 하겠습니다.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

म 실행할 때이 응용 프로그램 및 액세스 하 고는 *"/ Dinners/만들기"* 만들기 동작 구현에서 아래와 같은 UI를 렌더링 합니다 브라우저 내에서 URL:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a>동작 메서드를 만들어 HTTP POST를 구현 합니다.

HTTP GET 메서드 버전을이 만들기 작업 구현 했습니다. 폼 post를 수행할 "저장" 단추를 클릭할 때는 */Dinners/만들기* URL, HTML 전송 &lt;입력&gt; HTTP POST 동사를 사용 하 여 값을 형성 합니다.

HTTP POST 동작을 이제 구현 해 보겠습니다 우리의 동작 메서드를 만듭니다. HTTP POST 시나리오를 처리 하는 것을 나타내는 "AcceptVerbs" 특성에 우리의 DinnersController를 오버 로드 된 "만들기" 작업 메서드를 추가 하 여 시작 합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

다양 한 방식으로 게시 된 폼 매개 변수는 HTTP POST를 사용 하도록 설정 "만들기" 메서드 내에서 액세스할 수 있습니다 있습니다.

한 가지 방법은 새 Dinner 개체를 만들고 사용 하 여 하는 *UpdateModel()* 도우미 메서드 (예: 편집 작업을 수행한) 게시 된 양식 값을 채웁니다. 우리의 DinnerRepository에 추가 하 고 데이터베이스에 유지 다음 사용자를 아래 코드를 사용 하 여 새로 만든된 Dinner 보여 주는 우리의 세부 정보 매크로를 리디렉션합니다 다음 했습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

또는 Dinner 개체 메서드 매개 변수로 취급 create () 동작 메서드에 했으므로 접근 방식을 사용할 수 있습니다. ASP.NET MVC 다음 자동으로 us에 대 한 새 Dinner 개체를 인스턴스화할 양식 입력을 사용 하 여 해당 속성을 채울 하 고이 동작 메서드에 전달:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

위의 작업 메서드에 우리의 ModelState.IsValid 속성을 확인 하 여 Dinner 개체 폼 게시 값으로 성공적으로 채워져가 있는지 확인 합니다. 없는 경우 false 변환 문제 입력이 반환 됩니다 (예: EventDate 속성에 대 한 "BOGUS"의 문자열), 문제가 발생 하는 경우이 동작 메서드에 다시 표시 되 고 하 고 있습니다.

입력된 값이 유효 하면 작업 메서드에 추가 하 고 새 저녁에는 DinnerRepository 저장 시도 합니다. Try/catch 블록 내에서이 작업을 래핑하고 다시 표시 되 고 (이 예외가 발생 하는 dinnerRepository.Save() 메서드)에서 비즈니스 규칙 위반 된 경우.

이 오류 처리 동작에서 동작을 보려면 요청할 수는 */Dinners/만들기* URL과 사용자에 게 새 저녁에 대 한 세부 정보입니다. 잘못 된 입력 또는 값 수와 같은 아래에 강조 표시 하는 오류와 함께 다시 표시 하려면 폼 만들기 발생 합니다.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

만들기 폼 정확히 동일한 유효성 검사 및 비즈니스 규칙을 편집 폼 구분 하지 않고이 방법을 확인 합니다. 이 유효성 검사 및 비즈니스 규칙은 모델에 정의 된 및 UI 또는 응용 프로그램의 컨트롤러 내에서 포함 되지 않은 때문입니다. 즉, म 나중에 변경/전개 될 수는 유효성 검사 또는 비즈니스 규칙에는 단일 배치 하 고 응용 프로그램에 적용 합니다. 하지 자동으로 모든 기존 관계를 수정 또는 새 규칙을 적용 하도록 동작 메서드를 만들거나 변경 하거나 내의 모든 코드는 편집 해야 합니다.

입력된 값을 수정 하 고 "저장" 단추를 클릭 하는 경우 다시 우리의 외에는 DinnerRepository, 성공 하 고 새 Dinner 데이터베이스에 추가 됩니다. 그런 다음 리디렉션됩니다에 */Dinners/세부 정보 / [id]* URL – 여기서 म 나타납니다 새로 만든된 저녁에 대 한 세부 정보:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a>Delete 지원

우리의 DinnersController에 "삭제" 지원을 이제 추가 해 보겠습니다.

#### <a name="the-http-get-delete-action-method"></a>HTTP GET Delete 동작 메서드

Delete 동작 메서드를 사용 하 여 HTTP GET 동작을 구현 하 여 먼저 하겠습니다. 다른 사용자가 방문 하면이 메서드가 호출 됩니다는 */Dinners/Delete / [id]* URL입니다. 다음은 구현이입니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

동작 메서드를 삭제할 Dinner를 검색 하려고 합니다. 있으면 Dinner 렌더링 보기 Dinner 개체에 기반 합니다. 개체가 존재 하지 않는 (또는 이미 삭제 되었습니다) 해당 하는 경우 "NotFound"를 렌더링 하는 뷰를 반환 우리의 "Details" 동작 메서드에 대 한 앞에서 만든 서식 파일을 봅니다.

Delete 동작 메서드 내에서 마우스 오른쪽 단추로 클릭 하 고 "뷰 추가" 상황에 맞는 메뉴 명령 선택 하 여 "삭제" 보기 템플릿을 만들 수 있습니다. "뷰 추가" 대화 상자 내에서 우리 합니다 나타내고 म 해당 모델로 템플릿 우리의 보기를 Dinner 개체를 전달 하는 빈 템플릿을 만들:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

"추가" 단추를 클릭 하면 Visual Studio는 우리의 "\Views\Dinners" 디렉터리 내에서 "Delete.aspx" 보기 템플릿 파일을 새를 us에 대 한 추가 합니다. 일부 HTML 및 코드 삭제 확인 화면을 구현 하는 서식 파일을 추가 하겠습니다 다음과 유사한:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

위의 코드는 삭제 될 Dinner 및 출력의 제목을 표시는 &lt;양식&gt; 요소 게시물 /Dinners/Delete / [id] URL에 최종 사용자가 내 "삭제" 단추를 클릭 합니다.

이 응용 프로그램 및 액세스를 실행할 때는 *"/ Dinners/Delete / [id]"* 유효한 저녁에 대 한 URL 개체 렌더링 아래와 같은 UI:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| **쪽 주제: 우리가 왜 게시물?** |
| --- |
| 궁금할 것 – 이유 무엇 일까요의 노력을 통해 한 &lt;양식&gt; 우리의 삭제 확인 화면 내에서? 이유 사용 하지 않는 표준 하이퍼링크 실제 삭제 작업을 수행 하는 동작 메서드에 연결 하 시겠습니까? 원인은 사용 하기 위해 웹 크롤러에 으로부터 보호 하 고 검색 Url을 검색 하 고 실수로 인해 삭제 될 때 링크를 따라 데이터가 엔진에 주의를 기울여야 합니다. HTTP GET 기반 Url 액세스/탐색 하 여 "안전한" 간주 되 고 올바른 따르지 다음 HTTP POST 것입니다. 항상 파괴적 단계로 넣기 또는 HTTP POST 요청 뒤에 있는 데이터 수정 작업에 있는지 확인 하는 것이 좋습니다. |

#### <a name="implementing-the-http-post-delete-action-method"></a>HTTP POST Delete 동작 메서드를 구현합니다.

म 삭제 확인 화면을 표시 하는 구현 하는 삭제 작업 메서드의 HTTP GET 버전을 사용할 수 있습니다. 최종 사용자가 "삭제" 단추를 클릭 하면 양식 post를 수행 합니다는 */Dinners/저녁 / [id]* URL입니다.

아래 코드를 사용 하는 delete 동작 메서드의 HTTP "POST" 동작을 이제 구현 해 보겠습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

Delete 동작 메서드를 사용 하 여의 HTTP POST 버전 dinner 삭제할 개체를 검색 하려고 합니다. 이 찾을 수 없습니다 (이미 삭제 된) 경우 "NotFound" 템플릿 우리의 렌더링 합니다. Dinner를 찾으면는 DinnerRepository에서 삭제 것입니다. 그러면 "삭제" 서식 파일을 렌더링합니다.

"삭제" 서식 파일을 구현 하는 작업 메서드를 마우스 오른쪽 단추로 클릭 알아보고 "뷰 추가" 상황에 맞는 메뉴를 선택 하겠습니다. 빈 템플릿을 수 (및 모델 강력한 형식의 개체를 사용 하지) 하 게 알아보고 "삭제" 우리의 뷰 이름을 지정 하겠습니다. 다음 일부 HTML 콘텐츠를 추가:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

म 실행할 때이 응용 프로그램 및 액세스 하 고는 *"/ Dinners/Delete / [id]"* 우리의 Dinner 렌더링할 개체 삭제 확인 유효한 저녁에 대 한 URL이 아래와 같은 화면:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

"삭제" 단추를 클릭 하는 HTTP POST 수행 됩니다는 */Dinners/Delete / [id]* Dinner 데이터베이스에서 삭제 되 고 템플릿 우리의 "삭제" 보기를 표시 하는 URL:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a>모델 바인딩 보안

ASP.NET MVC의 기본 제공 모델 바인딩 기능을 사용 하는 두 가지 방법에 설명 했습니다. 먼저 UpdateModel() 메서드를 사용 하 여 기존 모델 개체에 대 한 속성을 업데이트 하 고 사용 하 여 두 번째 모델 개체의 동작 메서드 매개 변수로 전달 하는 것에 대 한 ASP.NET MVC 지원 합니다. 이러한 두 기술 모두는 매우 강력 하 고 매우 유용 합니다.

이 전원 함께 부분도 책임입니다. 항상 지나친 보안에 대 한 사용자 입력을 허용 하는 경우 해야 되며이 또한 쌍 양식 입력 개체에 바인딩할 때. 신경을 써야 항상 HTML로 인코드 HTML 및 JavaScript 주입 공격을 방지 하 고 SQL 주입 공격의 주의 해야 사용자가 입력 한 값 (참고: 샘플 응용 프로그램에서는이 방지 하기 위해 매개 변수를 자동으로 인코딩하는 방법에 대 한 LINQ to SQL 사용 유형의 공격)입니다. 하지 단독으로 유효성 검사는 클라이언트 쪽에 의존 하 고 항상 해커 보 거 스 값을 보내려는 시도 방지 하는 서버 쪽 유효성 검사를 사용 해야 합니다.

ASP.NET MVC의 바인딩 기능을 사용 하는 경우에 대해 고려해 야 확인을 추가 보안 항목에 바인딩하는 개체의 범위입니다. 특히, 바인딩될 수 있으며 실제로 업데이트를 최종 사용자가 업데이트할 수 있어야 하는 속성을만 허용 하는지 확인을 허용 하는 속성의 보안 의미를 이해 하 고 있는지 확인 하려고 합니다.

기본적으로 UpdateModel() 메서드 들어오는 폼 매개 변수 값과 일치 하는 모델 개체에 포함 된 모든 속성을 업데이트 하려고 합니다. 마찬가지로, 기본적으로도 작업 메서드 매개 변수로 전달 된 개체의 모든 형식 매개 변수를 통해 설정의 속성 있을 수 있습니다.

#### <a name="locking-down-binding-on-a-per-usage-basis"></a>사용량 기준 별로 바인딩 잠그는 기능이

제공 하는 명시적 "include 목록" 업데이트할 수 있는 속성의 바인딩 정책에는 사용량 기준으로 잠글 수 있습니다. 아래와 같은 UpdateModel() 방법이에 추가 문자열 배열 매개 변수를 전달 하 여이 작업을 수행할 수 있습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

또한 작업 메서드 매개 변수로 전달 된 개체는 "포함 목록"의 속성을 아래와 같은 지정을 사용할 수 있도록 [Bind] 속성을 지원 합니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a>바인딩 형식에 기초를 잠그는

또한 형식별으로 대 한 바인딩 규칙을 잠글 수 있습니다. 이 옵션을 사용 하면 한 번 바인딩 규칙을 지정 하 고 다음 모든 컨트롤러 및 작업 메서드를 통해 모든 시나리오 (UpdateModel 및 시나리오 둘 다 동작 메서드 매개 변수 포함)에 적용 되도록 할 수 있습니다.

형식으로 [바인드] 특성을 추가 하거나 (유형이 없으십니까 시나리오에 유용) 응용 프로그램의 Global.asax 파일 내에서 등록 하 여 형식당 하나의 바인딩 규칙을 사용자 지정할 수 있습니다. Include 바인딩 특성을 사용할 수 있습니다 및 어떤 속성을 제어 하려면 제외 속성은 특정 클래스 또는 인터페이스에 대 한 바인딩 가능한 합니다.

저녁 클래스에 대 한이 방법을 사용 하 여 업그레이드 되었으며 수정 응용 프로그램에서는 알아보고 [바인드] 특성 다음에 바인딩 가능한 속성 목록은 제한 하는 것을 추가 하겠습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

통해 바인딩, 조작할 수 않으십니까 컬렉션을 허용 하지 않는 것을 확인 하거나 DinnerID 또는 HostedBy 속성을 통해 바인딩을 설정할 수 있도록 했습니다. 보안상의 이유로 म 것 대신만 조작 작업 메서드 내에서 명시적 코드를 사용 하 여 이러한 특정 속성입니다.

### <a name="crud-wrap-up"></a>CRUD 래핑

ASP.NET MVC에는 다양 한 폼 게시 시나리오를 구현 하는 데 도움이 되는 기본 제공 기능이 포함 되어 있습니다. 우리의 DinnerRepository 위에 CRUD UI 지원을 제공 하는 다양 한 이러한 기능을 사용 했습니다.

응용 프로그램을 구현 하는 모델 중심 접근 방법을 사용 합니다. 즉,이 모든 유효성 검사 및 비즈니스 규칙 논리는 컨트롤러 또는 뷰를 그리고 우리의 모델 계층 – 내에서 정의 됩니다. 컨트롤러 클래스도 아니고 우리의 템플릿 보기 Dinner 모델 클래스에 의해 강제 적용 하는 특정 비즈니스 규칙에 대 한 정보가 있습니다.

정리 가이드 응용 프로그램의 아키텍처를 유지 하 고 쉽게 테스트할 수 있도록이 합니다. 비즈니스 규칙을 추가로 우리의 모델 계층을 나중에 추가할 수 있습니다 및 *코드 변경을 수행 하지 않아도* 우리의 컨트롤러 또는 뷰에 대 한 지원 해야 하 합니다. 이를 상당한 민첩성을 발전 하 고 나중에 응용 프로그램을 변경 하려고 합니다.

우리의 DinnersController 이제 Dinner 목록/세부 정보를 사용 하면으로 만들고 편집 하 고 delete 지원입니다. 아래는 클래스에 대 한 전체 코드를 찾을 수 있습니다.

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a>다음 단계

기본 CRUD (만들기, 읽기, 업데이트 및 삭제) 지원을 나타내는 DinnersController 클래스 내에서 구현 했습니다.

이제 살펴보겠습니다 ViewData 및 ViewModel 클래스는 폼에도 다양 한 UI를 사용 하도록 설정 하려면 사용 하는 방법을.

>[!div class="step-by-step"]
[이전](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
[다음](use-viewdata-and-implement-viewmodel-classes.md)
