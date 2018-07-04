---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: '2 부: 컨트롤러 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 2 부에서는 컨트롤러를 설명합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: a854feff675cae302b9927d209808257b7d087cb
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37381805"
---
<a name="part-2-controllers"></a>2 부: 컨트롤러
====================
[Jon Galloway](https://github.com/jongalloway)

> MVC Music Store 자습서 응용 프로그램을 소개 하 고 웹 개발을 위한 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 설명 됩니다.  
>   
> MVC Music Store는 온라인 음악 앨범을 판매 하 고 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.  
>   
> 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 2 부에서는 컨트롤러를 설명합니다.


기존 웹 프레임 워크를 들어오는 Url은 일반적으로 디스크에 파일이 매핑됩니다. 예를 들어:와 같은 URL에 대 한 요청을 "/ 대" 하거나 "/ Products.php" "Products.aspx" 또는 "Products.php" 파일에서 처리 될 수 있습니다.

웹 기반 MVC 프레임 워크를 약간 다른 방식으로 서버 코드에 Url을 매핑합니다. 대신 들어오는 Url 파일을 대신 매핑할 Url 클래스의 메서드. 이러한 클래스는 "컨트롤러" 라고 하 고 사용자 입력을 처리 하는 들어오는 HTTP 요청을 처리 하는 일을 담당 하는 클라이언트 다시 검색, 데이터 저장 및 전송에 대 한 응답 결정 (HTML 표시 파일을 다운로드, 다른 리디렉션 URL 등)입니다.

## <a name="adding-a-homecontroller"></a>HomeController를 추가합니다.

MVC Music Store 응용 프로그램 사이트의 홈 페이지 Url을 처리 하는 컨트롤러 클래스를 추가 하 여 시작 됩니다. ASP.NET MVC의 기본 명명 규칙을 준수 하 고 HomeController 호출 됩니다.

솔루션 탐색기 내에서 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 하 고 [추가]를 선택한 다음 "컨트롤러..." 명령을 선택 합니다.

![](mvc-music-store-part-2/_static/image1.jpg)

"컨트롤러 추가" 대화 상자가 표시 됩니다. "HomeController" 컨트롤러 이름과 추가 단추를 누릅니다.

![](mvc-music-store-part-2/_static/image1.png)

다음 코드를 사용 하 여 새 파일을 HomeController.cs에서 만들어집니다.

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

최대한 간단를 시작 하려면 보겠습니다 문자열로 반환 하는 간단한 메서드를 사용 하 여 인덱스 메서드를 대체 합니다. 두 가지 변경을 수행 됩니다.

- ActionResult 대신 문자열을 반환 하도록 메서드를 변경
- "Hello에서 홈" 반환할 return 문을 변경 합니다.

이제 메서드를 다음과 같이 표시 됩니다.

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a>응용 프로그램 실행

이제 사이트를 실행 해 보겠습니다. 수는 웹 서버를 시작 하 고 다음 중 하나를 사용 하 여 사이트를 사용해::

- 디버그 ⇨ 디버깅 시작 메뉴 항목 선택
- 도구 모음에서 녹색 화살표 단추를 클릭 합니다. ![](mvc-music-store-part-2/_static/image2.jpg)
- 바로 가기, F5 키를 사용 합니다.

위의 단계를 사용 하 여 프로젝트를 컴파일 및 시작 하려면 Visual Web Developer에 기본 제공 되는 ASP.NET Development Server 인해 합니다. 알림을, ASP.NET Development Server를 시작 했음을 나타내기 위해 화면 하단 모서리에 나타나고 포트 번호를 표시 하에서 실행 됩니다.

![](mvc-music-store-part-2/_static/image2.png)

Visual Web Developer는 웹 서버를 가리키는 URL 브라우저 창을 엽니다 자동으로 됩니다. 이렇게 하면 웹 응용 프로그램을 신속 하 게 사용해 주세요.

![](mvc-music-store-part-2/_static/image3.png)

알겠습니다. 아주 빠른-새 웹 사이트를 만들었습니다를 선 함수를 추가 하 고 브라우저에서 텍스트를 만들었습니다. Rocket 과학 하지 이지만 시작 합니다.

*참고: Visual Web Developer에 임의 무료 "port" 웹 사이트를 실행 하는 ASP.NET Development Server를 포함 합니다. 위의 스크린샷에서 사이트에서 실행 되 `http://localhost:26641/`이므로 26641 포트를 사용 하는 것입니다. 포트 번호에는 이와 다릅니다. 이 자습서에서는 like /Store/Browse URL에 대 한 이야기 하는 포트 번호 뒤 이동 됩니다. 26641 포트 번호를 가정 하 고/저장소/찾아보기로 이동 의미를 찾아 `http://localhost:26641/Store/Browse`합니다.*

## <a name="adding-a-storecontroller"></a>StoreController 추가

사이트의 홈 페이지를 구현 하는 간단한 HomeController 추가 했습니다. 지금 사용 하 여 음악 스토어의 검색 기능을 구현 하는 다른 컨트롤러를 추가 해 보겠습니다. 저장소 컨트롤러는 세 가지 시나리오를 지원 해야 합니다.

- 음악 스토어에서 음악 장르 목록 페이지
- 특정 장르에 음악 앨범의 모든를 나열 하는 찾아보기 페이지
- 특정 음악 앨범에 대 한 정보를 보여 주는 세부 정보 페이지

새 StoreController 클래스를 추가 하 여 시작 하겠습니다... 이미 않았다면 브라우저를 닫거나 디버그 ⇨ 디버깅 중지 메뉴 항목을 선택 하 여 응용 프로그램 실행을 중지 합니다.

이제 새 StoreController를 추가 합니다. HomeController를 사용 하 여 수행한 것 처럼에서는 이렇게 솔루션 탐색기 내에서 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 하 고 추가-&gt;컨트롤러 메뉴 항목

![](mvc-music-store-part-2/_static/image4.png)

이 새 StoreController는 "Index" 메서드가 이미 있습니다. 음악 스토어에서 모든 장르를 나열 하는 목록 페이지를 구현 하려면이 "Index" 메서드가 사용 하겠습니다. 두 가지 다른 시나리오를 처리 하는 StoreController 원하는 구현 하는 두 개의 추가 메서드 추가: 찾아보기 및 세부 정보입니다.

컨트롤러 내에서 이러한 메서드 (인덱스, 찾아보기 및 세부 정보) "컨트롤러 작업" 라고 이며 HomeController.Index () 작업 메서드를 사용 하 여 이미 살펴보았듯이, 업무 URL 요청에 응답 하 고 (일반적) 콘텐츠를 확인 하려면 브라우저 또는 URL을 호출 하는 사용자에 게 다시 전송 되어야 합니다.

TheIndex() "Hello에서 Store.Index()" 문자열을 반환 하는 방법을 변경 하 여 StoreController 구현을 먼저 및 browse () 및 Details() 이와 유사한 메서드 추가:

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

프로젝트를 다시 실행 하 고 다음 Url을 이동 합니다.

- / 저장소
- / 저장소/찾아보기
- / 저장소/세부 정보

이러한 Url 액세스 컨트롤러 내의 작업 메서드를 호출 되며 문자열 응답을 반환 합니다.

![](mvc-music-store-part-2/_static/image5.png)

잘 되는 되지만 이러한 방금 상수 문자열입니다. 보겠습니다 있도록 동적 URL에서 정보를 사용 하 고 페이지 출력에 표시할 수 있도록 합니다.

먼저 URL에서 쿼리 문자열 값을 검색 하는 찾아보기 작업 메서드를 변경 됩니다. 이 동작 메서드에 "장르" 매개 변수를 추가 하 여이 작업을 수행 수입니다. 이 작업을 수행 하는 경우 ASP.NET MVC는 모든 쿼리 문자열 또는 폼 post 라는 매개 변수 "장르"는 작업 메서드를 호출 하면 자동으로 전달 합니다.

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

*참고: HttpUtility.HtmlEncode 유틸리티 메서드를 사용 하 여 사용자 입력을 삭제 하는 것입니다. 이로써 /Store/Browse와 같은 링크를 사용 하 여 뷰에 Javascript 주입에서 사용자? 장르 =&lt;스크립트&gt;window.location = 'http://hackersite.com'&lt;/script&gt;합니다.*

이제/저장소 / 찾아보기 탐색 해 보겠습니다. 장르 Disco =

![](mvc-music-store-part-2/_static/image6.png)

보겠습니다 읽고 ID 라는 이름의 입력된 매개 변수를 표시 하는 세부 정보 작업을 다음 변경 이전 메서드와 달리 쿼리 문자열 매개 변수로 ID 값을를 포함 하지 않습니다. 대신 URL 자체 내에서 직접 포함 됩니다 것입니다. 예를 들어: /Store/Details/5 합니다.

ASP.NET MVC 쉽게 아무 것도 구성 하지 않고도 이렇게 할 수 있습니다. ASP.NET MVC의 기본 라우팅 규칙 작업 메서드 이름 뒤에 "ID" 라는 매개 변수를 URL의 세그먼트를 처리 하는 것입니다. 동작 메서드에서 ID 라는 매개 변수가 있으면 다음 ASP.NET MVC는 자동으로 URL 세그먼트를 매개 변수로 전달 합니다.

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

응용 프로그램을 실행 하 고 /Store/Details/5를 이동 합니다.

![](mvc-music-store-part-2/_static/image7.png)

지금까지 수행한 지금 정리해 보겠습니다.

- Visual Web Developer에서 새 ASP.NET MVC 프로젝트를 만들었습니다.
- ASP.NET MVC 응용 프로그램의 기본 폴더 구조에 설명 했습니다.
- ASP.NET Development Server를 사용 하 여 웹 사이트를 실행 하는 방법을 알게합니다
- 두 컨트롤러 클래스를 만들었습니다: HomeController 및는 StoreController
- URL 요청에 응답 하 고 브라우저에 텍스트를 반환 하는 컨트롤러 작업 메서드에 추가 했습니다.


> [!div class="step-by-step"]
> [이전](mvc-music-store-part-1.md)
> [다음](mvc-music-store-part-3.md)
