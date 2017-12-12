---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: "2 단계: 컨트롤러 | Microsoft Docs"
author: jongalloway
description: "이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 2 부에서는 컨트롤러에 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: bdafd751e996e759d516d0fa25b09eff21241ed7
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="part-2-controllers"></a>2 부: 컨트롤러
====================
으로 [Jon Galloway](https://github.com/jongalloway)

> MVC Music Store는 소개 하 고 웹 개발에 대 한 ASP.NET MVC와 Visual Studio를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램.  
>   
> MVC Music Store는 온라인 음악 앨범 판매 및 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.  
>   
> 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 2 부에서는 컨트롤러에 설명 합니다.


기존 웹 프레임 워크와 함께 들어오는 Url은 일반적으로 디스크 파일에 매핑됩니다. 예: URL에 대 한 요청 같은 "/ Products.aspx" 또는 "/ Products.php" "Products.aspx" 또는 "Products.php" 파일에서 처리 될 수 있습니다.

웹 기반 MVC 프레임 워크를 약간 다른 방식으로 서버 코드에 Url을 매핑합니다. 파일에 들어오는 Url 매핑, 대신 대신 Url에 매핑되는지 클래스에 대 한 메서드. 이러한 클래스는 "컨트롤러" 라고 하 고 사용자 입력을 처리 하는 들어오는 HTTP 요청을 처리 해야 하는, 검색 및 데이터를 저장 및 보내기에 대 한 응답을 결정 하는 클라이언트에 다시 (HTML을 표시, 파일을 다운로드, 다른 리디렉션 URL, 등)입니다.

## <a name="adding-a-homecontroller"></a>HomeController 추가

사이트의 홈 페이지 Url을 처리 하는 컨트롤러 클래스를 추가 하 여 MVC 음악 스토어 응용 프로그램을 먼저 실행 하겠습니다. ASP.NET MVC의 기본 명명 규칙에 따라 알아보고 HomeController 호출 하겠습니다.

솔루션 탐색기 내에서 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 하 고 "추가" 및 "컨트롤러..."를 선택 합니다. 명령입니다.

![](mvc-music-store-part-2/_static/image1.jpg)

이 "컨트롤러 추가" 대화 상자를 표시 합니다. "HomeController" 컨트롤러 이름을 지정 하 고 추가 단추를 누릅니다.

![](mvc-music-store-part-2/_static/image1.png)

HomeController.cs, 새 파일을 다음 코드로 만들어집니다.

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

가능한 한 간단 하 게 시작 하는 문자열만 반환 하는 간단한 방법을 인덱스 메서드를 바꿉니다 보겠습니다. 두 가지 변경을 수행 합니다.

- ActionResult 대신 문자열을 반환 방법 변경
- 반환할 Hello에서 "홈" return 문을 변경 합니다.

메서드는 이제 다음과 같이 표시 됩니다.

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a>응용 프로그램 실행

이제 사이트를 확인해 보겠습니다. 웹 서버를 시작 하 고 다음 중 하나를 사용 하는 사이트를 체험할 수 있습니다::

- 디버그 ⇨ 디버깅 시작 메뉴 항목 선택
- 도구 모음에서 녹색 화살표 단추를 클릭 합니다.![](mvc-music-store-part-2/_static/image2.jpg)
- 바로 가기 키, f5 키를 사용 합니다.

위의 단계를 사용 하 여이 프로젝트를 컴파일하 되 고 그러면 ASP.NET Development Server를 시작 하려면 Visual Web Developer에 기본 제공 됩니다. 알림을, ASP.NET Development Server가 시작 되었음을 나타내기 위해 화면 아래에 나타나고에서 실행 되 고 있는지 포트 번호가 표시 됩니다.

![](mvc-music-store-part-2/_static/image2.png)

Visual Web Developer 웹 서버를 가리키는 URL 브라우저 창을 엽니다 자동으로 됩니다. 이렇게 하면를 웹 응용 프로그램을 신속 하 게 시험해 수: 있습니다.

![](mvc-music-store-part-2/_static/image3.png)

알겠습니다 상당히 빠른-새 웹 사이트에서 만든 했던 삼 선 함수를 추가 하 고 브라우저에서 텍스트 설명 했습니다. 로켓 과학 하지 이지만 시작 합니다.

*참고: Visual Web Developer 웹 사이트 포트"임의의 무료" 번호에서 실행 ASP.NET 개발 서버를 포함 합니다. 또한 위의 스크린 샷에서 사이트에서 실행 중인 `http://localhost:26641/`, 26641 포트를 사용 하 고 있습니다. 포트 번호 달라 집니다. 이 자습서에서는 like /Store/Browse URL에 대해 논의할 하는 포트 번호 뒤 이동 됩니다. 26641의 포트 번호를 가정할 때/저장소/찾아보기로 이동은 의미를 찾아 `http://localhost:26641/Store/Browse`합니다.*

## <a name="adding-a-storecontroller"></a>StoreController 추가

사이트의 홈 페이지를 구현 하는 간단한 HomeController 추가 했습니다. 이제 음악 스토어의 검색 기능을 구현 하는을 사용 해야 하는 다른 컨트롤러를 추가 해 보겠습니다. 저장소 컨트롤러는 세 가지 시나리오를 지원 해야 합니다.

- 음악 스토어에서 음악 장르 목록 페이지
- 특정 장르의 음악 앨범을 모두 나열 하는 찾아보기 페이지
- 특정 음악 앨범에 대 한 정보를 표시 하는 세부 정보 페이지

새 StoreController 클래스를 추가 하 여 시작 합니다... 아직 하지 않는 경우 브라우저를 닫거나 디버그 ⇨ 디버깅 중지 메뉴 항목을 선택 하 여 응용 프로그램 실행을 중지 합니다.

이제 새 StoreController를 추가 합니다. 솔루션 탐색기 내에서 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 기능 선택 하 여 수행 됩니다 HomeController 사용 했던 것 처럼&gt;컨트롤러 메뉴 항목

![](mvc-music-store-part-2/_static/image4.png)

새 우리의 StoreController "Index" 메서드가 이미 있습니다. 음악 스토어에서 모든 장르를 나열 하는 가격 목록 페이지를 구현 하려면이 "Index" 메서드를 사용 합니다. 시나리오를 구현 하는 두 개의 다른 우리의 StoreController 처리 하기 원하는 두 개의 추가 메서드 추가: 찾아보기 및 세부 정보입니다.

컨트롤러 내에서 이러한 메서드 (인덱스, 찾아보기 및 세부 정보)에 "컨트롤러 작업" 라고 하며 HomeController.Index () 동작 메서드로 앞서 설명한 바가 작업 하는 것 (일반적) 콘텐츠를 확인 하 고 URL 요청에 응답 브라우저 또는 URL을 호출 하는 사용자에 게 다시 전송 되어야 합니다.

StoreController 구현은 theIndex() "Hello에서 Store.Index()" 문자열을 반환 하는 방법을 변경 하 여 시작 합니다 및 browse () 및 Details() 비슷한 메서드를 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

프로젝트를 다시 실행 하 고 다음 Url을 탐색 합니다.

- / 저장소
- / 저장소/찾아보기
- / 저장소/세부 정보

이러한 Url에 액세스 컨트롤러 내에서 작업 메서드를 호출 하 고 문자열 응답 반환 됩니다.

![](mvc-music-store-part-2/_static/image5.png)

아니지만 방금 상수 문자열입니다. 보겠습니다 있도록 동적으로 URL에서 정보를 가져올 없도록 페이지 출력에 표시 합니다.

먼저 URL에서 쿼리 문자열 값을 검색 하는 찾아보기 동작 메서드를 변경 합니다. 이 동작 메서드에 "장르" 매개 변수를 추가 하 여 하겠습니다. 이 작업을 수행 하는 경우 ASP.NET MVC가 호출 되 면이 동작 메서드에 "장르" 라는 모든 쿼리 문자열 또는 폼 게시 매개를 자동으로 전달 합니다.

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

*참고:에서는 HttpUtility.HtmlEncode 유틸리티 메서드를 사용자 입력을 삭제 합니다. 따라서 사용자를 /Store/Browse 같은 링크와 함께 보기에 Javascript를 삽입 수 없습니다. 장르 =&lt;스크립트&gt;window.location= 'http://hackersite.com'&lt;/script&gt;합니다.*

이제/저장소/찾아보기를 찾아보겠습니다? Genre Disco =

![](mvc-music-store-part-2/_static/image6.png)

이제 다음 변경 상세 작업 읽고 입력된 매개 변수를 표시 하 라는 id입니다. 이 이전 메서드와 달리 쿼리 문자열 매개 변수로 ID 값을 포함 하지 않습니다. 대신 URL 자체 내에서 직접 포함할 것 했습니다. 예를 들어: /Store/Details/5 합니다.

ASP.NET MVC를 통해이 이상 구성할 필요 없이 쉽게 수행할 수 있습니다. ASP.NET MVC의 기본 라우팅 규칙 동작 메서드 이름 뒤에 오는 "ID" 라는 매개 변수를 URL의 세그먼트를 처리 하는 것입니다. 작업 메서드에 매개 변수 ID 이름 경우 다음 ASP.NET MVC는 자동으로 URL 세그먼트를 매개 변수로 전달 합니다.

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

응용 프로그램을 실행 하 고 /Store/Details/5로 이동 합니다.

![](mvc-music-store-part-2/_static/image7.png)

지금까지 수행한 무엇 요약해 보면:

- Visual Web Developer에서 새 ASP.NET MVC 프로젝트를 만들었습니다.
- ASP.NET MVC 응용 프로그램의 기본 폴더 구조에 설명 했습니다.
- ASP.NET 개발 서버를 사용 하 여 웹 사이트를 실행 하는 방법을 배웠습니다.
- 두 개의 컨트롤러 클래스 만들었습니다:는 HomeController 및는 StoreController
- 작업 메서드는 URL 요청에 응답 하 고 브라우저에 텍스트를 반환 합니다.이 컨트롤러를 추가 했습니다.


>[!div class="step-by-step"]
[이전](mvc-music-store-part-1.md)
[다음](mvc-music-store-part-3.md)
