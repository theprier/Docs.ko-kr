---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: ASP.NET Web API 사용 하 여 RESTful Api 빌드 | Microsoft Docs
author: rick-anderson
description: 최근 몇 년 동안 HTTP HTML 페이지를 제공 하는 데 아닌지 지우기 사항이 되었습니다. 소수의 o를 사용 하 여 웹 Api를 구축 하기 위한 강력한 플랫폼 이기도 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: cb02288e93be801a1e55852741ed1443d8d3617d
ms.sourcegitcommit: 3a893ae05f010656d99d6ddf55e82f1b5b6933bc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/18/2018
---
<a name="build-restful-apis-with-aspnet-web-api"></a>ASP.NET Web API 사용 하 여 RESTful Api 빌드
====================
으로 [웹 캠프 팀](https://twitter.com/webcamps)

> 최근 몇 년 동안 HTTP HTML 페이지를 제공 하는 데 아닌지 지우기 사항이 되었습니다. 와 같은 몇 가지 간단한 개념 더하기는 소수의 동사 (GET, POST 등)을 사용 하는 웹 Api를 구축 하기 위한 강력한 플랫폼 이기도 *Uri* 및 *헤더*합니다. ASP.NET Web API는 HTTP 프로그래밍을 단순화 하는 구성 요소 집합입니다. ASP.NET MVC 런타임 기반의 빌드하 때문에 Web API http 전송 낮은 수준의 세부 정보를 자동으로 처리 합니다. 같은 시간에 Web API HTTP 프로그래밍 모델을 자연스럽 게 표시합니다. 사실, 하나의 웹 API의 ´ ֲ *하지* HTTP 현실을 추상화 합니다. 결과적으로, 웹 API는 유연 하 고 쉽게 확장할 수 있습니다. 이 실습 랩에서 연락처 관리자 응용 프로그램에 대 한 간단한 REST API를 만들려는 웹 API를 사용 합니다. 또한 API를 사용 하는 클라이언트를 작성 합니다. REST 아키텍처 스타일은 분명 하지 않지만 HTTP에 대 한 유효한 접근 방법 HTTP-활용 하는 효과적인 방법을 것으로 입증 된 합니다. 연락처의 관리자는 RESTful 적용, 추가 및 제거 등의 연락처에 대 한 노출 합니다. 이 랩에서 HTTP, REST, 기본적으로 이해 하며 HTML, JavaScript 및 jQuery 대 한 기본 실무 지식이 있다고 가정 합니다.
> 
> > [!NOTE]
> > ASP.NET 웹 사이트에 ASP.NET Web API 프레임 워크에서 전용 영역 [ https://asp.net/web-api ](https://asp.net/web-api)합니다. 이 사이트를 계속 최신 정보, 샘플 및 웹 API와 관련 된 뉴스 있으므로 체크 자주 제공할 거의 모든 장치 또는 개발 프레임 워크를 사용할 수 있는 사용자 지정 웹 Api를 만드는 아트를 철저히 하려는 경우.
> > 
> > ASP.NET Web API, ASP.NET MVC 4 비슷합니다 사용 가능한 종속성 주입 프레임 워크의 여러 상당히 쉽게 사용할 수 있도록 하는 컨트롤러에서 서비스 계층을 구분 측면에서 뛰어난 유연성을 있습니다. MSDN에서 다운로드할 수 있는 ASP.NET Web API 프로젝트에서 종속성 주입을 위한 Ninject를 사용 하는 방법을 보여 주는 좋은 예제 중인 있고 [여기](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)합니다.
> 
> 
> 모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)합니다.


<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서 배웁니다 하는 방법:

- RESTful 웹 API를 구현 합니다.
- HTML 클라이언트에서 API를 호출 합니다.

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

다음은이 실습 랩을 완료 하려면 필요 합니다.

- [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽기 [부록 B](#AppendixB) 설치 하는 방법에 대 한 지침은).

<a id="Setup"></a>
### <a name="setup"></a>설정

**설치 하는 코드 조각**

편의 위해는이 랩에 따라 관리 코드의 대부분 Visual Studio 코드 조각 수 있습니다. 실행 코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.

이 문서에서 부록을 참조할 수 사용 하는 방법에 알아봅니다 사용 하 고 Visual Studio 코드 조각에 익숙한 경우 &quot; [부록 a:를 사용 하 여 코드 조각을](#AppendixA)&quot;합니다.

<a id="Exercises"></a>
## <a name="exercises"></a>연습

이 실습 랩에서 다음 연습에 포함 됩니다.

1. [연습 1: 읽기 전용 웹 API 만들기](#Exercise1)
2. [연습 2: 읽기/쓰기 Web API 만들기](#Exercise2)
3. [연습 3: HTML 클라이언트에서 Web API를 사용 합니다.](#Exercise3)

> [!NOTE]
> 각 연습 동반 되는 **끝** 연습을 완료 한 후 가져와야 생성 되는 솔루션에 포함 된 폴더입니다. 연습을 통해 작업 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.


예상 소요 시간: **60 분**합니다.

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a>연습 1: 읽기 전용 웹 API 만들기

이 연습에서는 연락처의 관리자에 대 한 읽기 전용 GET 메서드를 구현 합니다.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a>작업 1-API 프로젝트 만들기

이 태스크에서는 Web API 웹 응용 프로그램을 만드는 새 ASP.NET 웹 프로젝트 템플릿을 사용 합니다.

1. 실행 **Visual Studio 2012 Express for Web**이 이동 작업을 수행 하는, **시작** 유형과 **VS Express for Web** 다음 키를 누릅니다 **Enter**합니다.
2. **파일** 메뉴 선택 **새 프로젝트**합니다. 선택 된 **Visual C# | 웹** 프로젝트 프로젝트 형식 트리 뷰에서 형식을 선택한 다음 선택에서 **ASP.NET MVC 4 웹 응용 프로그램** 프로젝트 형식을 합니다. 프로젝트의 설정 **이름** 를 *ContactManager* 및 **솔루션 이름** 를 *시작*, 클릭 **확인**.

    ![새 ASP.NET MVC 4.0 웹 응용 프로그램 프로젝트를 만드는](build-restful-apis-with-aspnet-web-api/_static/image1.png "새 ASP.NET MVC 4.0 웹 응용 프로그램 프로젝트 만들기")

    *새 ASP.NET MVC 4.0 웹 응용 프로그램 프로젝트 만들기*
3. ASP.NET MVC 4 프로젝트 형식 대화 상자에서 선택 된 **웹 API** 프로젝트 유형입니다. **확인**을 클릭합니다.

    ![웹 API 프로젝트 형식 지정](build-restful-apis-with-aspnet-web-api/_static/image2.png "웹 API 프로젝트 형식 지정")

    *웹 API 프로젝트 형식 지정*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a>작업 2-연락처 관리자 API 컨트롤러 만들기

이 작업에서는 API 메서드 상주할 컨트롤러 클래스를 만듭니다.

1. 라는 파일을 삭제 **ValuesController.cs** 내 **컨트롤러** 프로젝트에서 폴더입니다.
2. 마우스 오른쪽 단추로 클릭는 **컨트롤러** 고 프로젝트에서 폴더 **추가 | 컨트롤러** 상황에 맞는 메뉴입니다.

    ![프로젝트에 새 컨트롤러 추가](build-restful-apis-with-aspnet-web-api/_static/image3.png "프로젝트에 새 컨트롤러 추가")

    *프로젝트에 새 컨트롤러 추가*
3. 에 **컨트롤러 추가** 나타나는 대화 상자 선택 **빈 API 컨트롤러** 템플릿 메뉴에서 합니다. 컨트롤러 클래스 이름을 **ContactController**합니다. 클릭 **추가 합니다.**

    ![컨트롤러 추가 대화 상자를 사용 하 여 새 Web API 컨트롤러를 만들려면](build-restful-apis-with-aspnet-web-api/_static/image4.png "컨트롤러 추가 대화 상자를 사용 하 여 새 Web API 컨트롤러를 만들려면")

    *컨트롤러 추가 대화 상자를 사용 하 여 새 Web API 컨트롤러를 만들려면*
4. 다음 코드를 추가 하는 **ContactController**합니다.

    (코드 조각- *웹 API 랩-Ex01-Get API 메서드*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. 키를 눌러 **F5** 응용 프로그램을 디버깅 합니다. 웹 API 프로젝트에 대 한 기본 홈 페이지가 표시 됩니다.

    ![ASP.NET Web API 응용 프로그램의 기본 홈 페이지](build-restful-apis-with-aspnet-web-api/_static/image5.png "ASP.NET Web API 응용 프로그램의 기본 홈 페이지")

    *ASP.NET Web API 응용 프로그램의 기본 홈 페이지*
6. Internet Explorer 창에서 눌러는 **F12** 키를 열려면는 **개발자 도구** 창. 클릭는 **네트워크** 탭을 클릭 한 다음는 **캡처 시작** 단추 창에 네트워크 트래픽 캡처를 시작 합니다.

    ![네트워크 탭을 열면 및 시작 네트워크 캡처](build-restful-apis-with-aspnet-web-api/_static/image6.png "네트워크 캡처 네트워크 탭을 열면 및 시작")

    *네트워크 탭을 열면 및 네트워크 캡처를 시작 합니다.*
7. 브라우저의 주소 표시줄에 URL 추가 **/api/연락처** 및 enter 키를 누릅니다. 네트워크 캡처 창에 전송 세부 정보가 표시 됩니다. 응답의 MIME 형식을 **응용 프로그램/json**합니다. 이 기본 출력 형식을 JSON을가 하는 방법을 보여 줍니다.

    ![네트워크 보기에는 웹 API 요청의 출력을 보는](build-restful-apis-with-aspnet-web-api/_static/image7.png "네트워크 보기에서 Web API 요청의 출력 보기")

    *네트워크 보기에서 Web API 요청의 출력 보기*

    > [!NOTE]
    > 이 시점에서 Internet Explorer 10의 기본 동작은 웹 API 호출 로부터 발생 스트림을 열거나 저장 하 시겠습니까 사용자에 게 됩니다. 출력을 웹 API URL 호출의 JSON 결과 포함 하는 텍스트 파일 됩니다. 개발자 도구 창을 통해 응답의 콘텐츠를 볼 수 있도록 대화 상자를 취소 하지 마십시오.
8. 클릭는 **자세히 보기로 이동** 이 API 호출의 응답에 대 한 자세한 내용을 보려면 단추입니다.

    ![자세히 보기를 전환할](build-restful-apis-with-aspnet-web-api/_static/image8.png "를 자세히 보기로 전환")

    *자세히 보기를 전환*
9. 클릭는 **응답 본문** 탭 실제 JSON 응답 텍스트를 볼 수 있습니다.

    ![네트워크 모니터의 텍스트 출력은 JSON 보기](build-restful-apis-with-aspnet-web-api/_static/image9.png "네트워크 모니터의 텍스트 출력은 JSON 보기")

    *네트워크 모니터에서 JSON 출력 텍스트를 보기*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a>작업 3-연락처 모델을 만드는 하 고 연락처 컨트롤러 보강

이 작업에서는 API 메서드 상주할 컨트롤러 클래스를 만듭니다.

1. 마우스 오른쪽 단추로 클릭는 **모델** 폴더를 선택 **추가 | 클래스 중...**  상황에 맞는 메뉴입니다.

    ![웹 응용 프로그램에 새 모델 추가](build-restful-apis-with-aspnet-web-api/_static/image10.png "웹 응용 프로그램에 새 모델 추가")

    *웹 응용 프로그램에 새 모델 추가*
2. 에 **새 항목 추가** 대화 상자에서 새 파일의 이름 **Contact.cs** 클릭 **추가 합니다.**

    ![새 연락처 클래스 파일을 만드는](build-restful-apis-with-aspnet-web-api/_static/image11.png "새 연락처 클래스 파일 만들기")

    *새 연락처 클래스 파일 만들기*
3. 다음 강조 표시 된 코드를 추가 하는 **연락처** 클래스입니다.

    (코드 조각- *웹 API 랩-Ex01-연락처 클래스*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. 에 **ContactController** 클래스, 단어를 선택 **문자열** 의 메서드 정의에 **가져오기** 메서드와 해당 단어 입력 *연락처*합니다. 표시기는 단어를으로 입력 되 면 단어의 시작 부분에 표시 됩니다 **연락처**합니다. 키를 누른 채 중 하나는 **Ctrl** 키 마침표 (.) 키를 누르거나 마우스를 사용 하 여 코드 편집기 자동으로 채울에서 지원 대화 상자를 열려면 아이콘을 클릭는 **를 사용 하 여** 는 모델에 대 한 지시문 네임 스페이스입니다.

    ![네임 스페이스 선언에 대 한 Intellisense 지원을 사용 하 여](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    *네임 스페이스 선언에 대 한 Intellisense 지원을 사용 하 여*
5. 에 대 한 코드를 수정는 **가져오기** 메서드 연락처 모델 인스턴스의 배열을 반환 하도록 합니다.

    (코드 조각- *웹 API 랩-Ex01-연락처 목록을 반환*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. 키를 눌러 **F5** 브라우저에서 웹 응용 프로그램을 디버깅 합니다. 변경 된 API의 응답 출력에를 보려면 다음 단계를 수행 합니다.

   1. 브라우저가 열리면 되 면 키를 눌러 **F12** 아직 개발자 도구 열려 있지 않은 경우.
   2. 클릭는 **네트워크** 탭 합니다.
   3. 키를 눌러는 **캡처 시작** 단추입니다.
   4. URL 접미사 추가 **/api/연락처** 누릅니다 주소 표시줄에서 URL로의 **Enter** 키입니다.
   5. 키를 눌러는 **자세히 보기로 이동** 단추입니다.
   6. 선택 된 **응답 본문** 탭 합니다. 연락처 인스턴스의 배열 serialize 된 형식을 나타내는 JSON 문자열로 표시 됩니다.

      ![JSON 직렬화는 복잡 한 Web API 메서드 호출의 출력](build-restful-apis-with-aspnet-web-api/_static/image13.png "JSON 직렬화는 복잡 한 Web API 메서드 호출의 출력")

      *복잡 한 Web API 메서드 호출의 JSON으로 직렬화 된 출력*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a>작업 4-서비스 계층에 기능을 압축 풀기

이 작업에서는 실제로 작업을 수행 하는 서비스를 다시 예외인 컨트롤러 계층에서 해당 서비스 기능을 분리 하 고 개발자가 쉽게 서비스 계층에 기능을 추출 하는 방법을 보여 줍니다.

1. 솔루션의 루트에서 새 폴더를 만들고 이름을 **서비스**합니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 **ContactManager** 프로젝트를 **추가** | **새 폴더**, 이름을 *서비스*합니다.

    ![Creating 서비스 폴더](build-restful-apis-with-aspnet-web-api/_static/image14.png "만드는 서비스 폴더")

    *서비스 폴더 만들기*
2. 마우스 오른쪽 단추로 클릭는 **서비스** 폴더를 선택 **추가 | 클래스 중...**  상황에 맞는 메뉴입니다.

    ![서비스 폴더에 새 클래스 추가](build-restful-apis-with-aspnet-web-api/_static/image15.png "서비스 폴더에 새 클래스 추가")

    *서비스 폴더에 새 클래스 추가*
3. 경우는 **새 항목 추가** 대화 상자가 나타나면 새 클래스의 이름을 **ContactRepository** 클릭 **추가**합니다.

    ![연락처 리포지토리 서비스 계층에 대 한 코드를 포함 하도록 클래스 파일을 만드는](build-restful-apis-with-aspnet-web-api/_static/image16.png "연락처 리포지토리 서비스 계층에 대 한 코드를 포함 하도록 클래스 파일 만들기")

    *연락처 리포지토리 서비스 계층에 대 한 코드를 포함 하도록 클래스 파일 만들기*
4. 사용 하 여 추가 지시문을 **ContactRepository.cs** 모델 네임 스페이스를 포함 하는 파일입니다.

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. 다음 강조 표시 된 코드를 추가 하는 **ContactRepository.cs** GetAllContacts 메서드를 구현 하는 파일입니다.

    (코드 조각- *웹 API 랩-Ex01-연락처 리포지토리에*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. 열기는 **ContactController.cs** 아직 열지 않은 경우에 파일입니다.
7. 다음 추가 문을 사용 하 여 파일의 네임 스페이스 선언 섹션에 있습니다.

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. 다음 강조 표시 된 코드를 추가 하는 **ContactController.cs** 서비스 구현의 멤버가 만들 수는 클래스의 나머지 부분에 사용 하 여 있도록 저장소의 인스턴스를 나타내는 전용 필드를 추가 하는 클래스입니다.

    (코드 조각- *Web API 랩-Ex01-연락처 컨트롤러*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. 변경 된 **가져오기** 을 메서드 연락처 저장소 서비스를 사용 합니다.

    (코드 조각- *웹 API 랩-Ex01-저장소를 통해 연락처 목록을 반환*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. 에 중단점을 설정의 **ContactController**의 **가져오기** 메서드 정의 합니다.

   ![연락처 컨트롤러에 중단점을 추가](build-restful-apis-with-aspnet-web-api/_static/image17.png "연락처 컨트롤러에 중단점을 추가 합니다.")

   *연락처 컨트롤러에 중단점을 추가합니다.*
11. **F5** 키를 눌러 응용 프로그램을 실행합니다.
12. 브라우저를 열 때 키를 눌러 **F12** 개발자 도구를 엽니다.
13. 클릭는 **네트워크** 탭 합니다.
14. 클릭는 **캡처 시작** 단추입니다.
15. 접미사가 있는 주소 표시줄에 URL 추가 **/api/연락처** 한 키를 누릅니다 **Enter** API 컨트롤러를 로드할 수 있습니다.
16. Visual Studio 2012를 한 번 나눌 **가져오기** 메서드 실행을 시작 합니다.

   ![Get 메서드 내에서 주요](build-restful-apis-with-aspnet-web-api/_static/image18.png "Get 메서드 내에서 분리")

   *Get 메서드 내에서 분리*
17. **F5**를 눌러 계속합니다.
18. 로 돌아갈 Internet Explorer 없는에 포커스가 있을 경우. 네트워크 캡처 창을 note 합니다.

    ![네트워크에서 Internet Explorer Web API 호출의 결과 보여 주는 보기](build-restful-apis-with-aspnet-web-api/_static/image19.png "네트워크 Web API 호출의 결과 보여 주는 Internet Explorer에서 보기")

    *Web API 호출의 결과 보여 주는 Internet Explorer에서 네트워크 보기*
19. 클릭는 **자세히 보기로 이동** 단추입니다.
20. 클릭는 **응답 본문** 탭 합니다. API 호출의 JSON 출력을 확인 하 고 서비스 계층에서 검색할 두 개의 연락처를 나타내는 방법입니다.

    ![개발자 도구 창에서 Web API의 JSON 출력을 보기](build-restful-apis-with-aspnet-web-api/_static/image20.png "개발자 도구 창에서 Web API의 JSON 출력 보기")

    *개발자 도구 창에서 Web API의 JSON 출력 보기*

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a>연습 2: 읽기/쓰기 Web API 만들기

이 연습에서는 POST 구현 및 데이터 편집 기능과 함께 사용 하도록 설정 하려면 연락처의 관리자에 대 한 PUT 메서드.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a>작업 1-웹 API 프로젝트 열기

이 태스크에서는 사용자 입력을 수락할 수 있도록 실습 1에서 만든 웹 API 프로젝트 향상을 위해 준비 합니다.

1. 실행 **Visual Studio 2012 Express for Web**이 이동 작업을 수행 하는, **시작** 유형과 **VS Express for Web** 다음 키를 누릅니다 **Enter**합니다.
2. 열기는 **시작** 솔루션에 있는 **소스/Ex02-ReadWriteWebAPI/시작/** 폴더입니다. 그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.

   1. 제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
3. 열기는 **Services/ContactRepository.cs** 파일입니다.

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a>작업 2-연락처 저장소 구현에 데이터 지 속성 기능 추가

이 작업을 유지 하 고 사용자 입력 및 새 연락처 인스턴스 수락 수 있도록 실습 1에서 만든 웹 API 프로젝트의 ContactRepository 클래스를 확장 됩니다.

1. 다음 상수를 추가 **ContactRepository** 를 웹 서버 캐시 항목 키 이름이이 연습 뒷부분에서의 이름을 나타내는 클래스입니다.

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. 생성자를 추가 **ContactRepository** 다음 코드를 포함 합니다.

    (코드 조각- *웹 API 랩-Ex02-연락처 리포지토리에 생성자*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. 에 대 한 코드를 수정 된 **GetAllContacts** 아래 설명 된 대로 메서드.

    (코드 조각- *웹 API 랩-Ex02-모든 연락처 가져오기*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > 이 예에서는 데모용 되며 값 세션 저장 메커니즘 또는 요청 저장소 수명을 사용 하지 않고 동시에 여러 클라이언트에 사용할 수는 있도록 저장 미디어로는 웹 서버의 캐시를 사용 합니다. Entity Framework, XML 저장소 또는 다른 다양 한 웹 서버 캐시 대신 사용할 수 하나.
4. 라는 새 메서드를 구현 **SaveContact** 에 **ContactRepository** 클래스를 저장 하는 연락처의 작업을 수행 합니다. **SaveContact** 메서드는 단일 취해야 **연락처** 성공 또는 실패를 나타내는 매개 변수 및 반환 하는 부울 값입니다.

    (코드 조각- *웹 API 랩-Ex02-SaveContact 메서드 구현*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a>연습 3: HTML 클라이언트에서 Web API를 사용 합니다.

이 연습에서는 웹 API를 호출 하는 HTML 클라이언트에 만들어집니다. 이 클라이언트는 JavaScript를 사용 하 여 웹 API와 데이터 교환을 이용 하 고 HTML 태그를 사용 하 여 웹 브라우저에서 결과 표시 합니다.

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a>작업 1-연락처를 표시 하기 위한 GUI를 제공 하 여 인덱스 뷰를 수정 합니다.

이 작업을 지원 하면 HTML 브라우저에 기존 연락처 목록을 표시 하기 위해 웹 응용 프로그램의 기본 인덱스 뷰를 수정 합니다.

1. 열고 **Visual Studio 2012 Express for Web** 열려 있지 않으면입니다.
2. 열기는 **시작** 솔루션에 있는 **소스/Ex03-ConsumingWebAPI/시작/** 폴더입니다. 그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.

   1. 제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
3. 열기는 **Index.cshtml** 에 있는 파일 **뷰/홈** 폴더입니다.
4. Id가 인 div 요소 내에서 HTML 코드를 바꿉니다 **본문** 다음 코드 처럼 표시 되도록 합니다.

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. 웹 API에 HTTP 요청을 수행 하는 파일의 맨 아래에 다음 Javascript 코드를 추가 합니다.

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. 열기는 **ContactController.cs** 아직 열지 않은 경우에 파일입니다.
7. 중단점을 배치는 **가져오기** 의 메서드는 **ContactController** 클래스입니다.

    ![API 컨트롤러의 Get 메서드에서 중단점을 배치한](build-restful-apis-with-aspnet-web-api/_static/image21.png "API 컨트롤러의 Get 메서드에서 중단점을 배치 합니다.")

    *API 컨트롤러의 Get 메서드에서 중단점을 배치합니다.*
8. 키를 눌러 **F5** 프로젝트를 실행 합니다. 브라우저는 HTML 문서를 로드 합니다.

    > [!NOTE]
    > 응용 프로그램의 루트 URL로 이동 하는 것을 확인 합니다.
9. 페이지가 로드 되 고 JavaScript 실행, 중단점이 적중 됩니다 및 컨트롤러에 코드 실행이 일시 중지 됩니다.

    ![VS Express를 사용 하 여 웹에 대 한 Web API 호출으로 디버깅](build-restful-apis-with-aspnet-web-api/_static/image22.png "VS Express for Web 사용 하 여 Web API 호출으로 디버깅")

    *Visual Studio 2012 Express for Web 사용 하 여 Web API 호출으로 디버깅*
10. 중단점 및 키를 눌러 제거 **F5** 또는 디버깅 도구 모음 **계속** 브라우저에서 보기를 로드 합니다. 계속 하려면 단추입니다. 웹 API 호출이 완료 되 면 호출 브라우저에서 목록 항목으로 표시 된 웹 API에서 반환 된 연락처 표시 되어야 합니다.

    ![목록 항목으로는 브라우저에 표시 되는 API 호출의 결과](build-restful-apis-with-aspnet-web-api/_static/image23.png "목록 항목으로는 브라우저에 표시 되는 API 호출의 결과")

    *목록 항목으로는 브라우저에 표시 되는 API 호출의 결과*
11. 디버깅을 중지합니다.

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a>작업 2-연락처 작성용 GUI를 제공 하 여 인덱스 뷰를 수정 합니다.

이 태스크에서는 MVC 응용 프로그램의 인덱스 뷰를 수정 하려면 계속 됩니다. 폼을 사용자 입력 캡처 되며 새 연락처를 만드는 웹 API에 전송 되는 HTML 페이지에 추가 됩니다 및 GUI에서 날짜를 수집 하는 새 Web API 컨트롤러 메서드 생성 됩니다.

1. 열기는 **ContactController.cs** 파일입니다.
2. 라는 컨트롤러 클래스에 새 메서드 추가 **Post** 다음 코드에 나와 있는 것 처럼 합니다.

    (코드 조각- *웹 API 랩-Ex03-Post 메서드*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. 열기는 **Index.cshtml** 열려 있지 않으면 Visual Studio에서 파일입니다.
4. 이전 태스크에서 추가한 순서가 지정 되지 않은 목록 바로 다음 파일에 아래 HTML 코드를 추가 합니다.

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. 문서 맨 아래에 스크립트 요소 내에서 데이터를 게시 Web API HTTP POST 호출을 사용 하는 단추 클릭 이벤트를 처리 하려면 다음 강조 표시 된 코드를 추가 합니다.

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. **ContactController.cs**, 중단점을 배치는 **Post** 메서드.
7. 키를 눌러 **F5** 브라우저에서 응용 프로그램을 실행 합니다.
8. 페이지는 브라우저에서 로드 되 면 새 연락처 이름 및 Id와 클릭에 입력 된 **저장** 단추입니다.

    ![브라우저에 HTML 클라이언트 문서 로드](build-restful-apis-with-aspnet-web-api/_static/image24.png "브라우저에 HTML 클라이언트 문서 로드")

    *브라우저에 로드 하는 클라이언트 HTML 문서*
9. 디버거 창 중단 시는 **Post** 메서드, 속성을 살펴보기는 **문의** 매개 변수입니다. 값 형식으로 입력 데이터를 일치 해야 합니다.

    ![클라이언트에서 Web API에 전송 되는 연락처 개체](build-restful-apis-with-aspnet-web-api/_static/image25.png "클라이언트에서 Web API에 전송 되는 연락처 개체")

    *클라이언트에서 Web API에 전송 되는 연락처 개체*
10. 될 때까지 디버거에서 메서드를 통해 단계는 **응답** 변수를 만들었습니다. 검사 되는 **지역** 디버거에서 창 표시 속성을 모두 설정 되어 있는지 합니다.

   ![디버거에서 만든 응답](build-restful-apis-with-aspnet-web-api/_static/image26.png "디버거에서 만든 응답")

   *디버거에서 만든 응답*
11. 키를 누르면 **F5** 키를 누르거나 **계속** 디버거 요청을 수행 합니다. 저장 하는 연락처 목록에 새 연락처를 추가한 브라우저에 다시 전환 하면는 **ContactRepository** 구현 합니다.

   ![브라우저를 성공적으로 만드는 새 연락처 인스턴스의 반영](build-restful-apis-with-aspnet-web-api/_static/image27.png "브라우저 반영 새 연락처 인스턴스를 성공적으로 만들기")

   *새 연락처 인스턴스의 성공적으로 만드는 반영 하는 브라우저*

> [!NOTE]
> 또한 Azure 다음에이 응용 프로그램을 배포할 수 있습니다 [부록 c: 게시 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램](#AppendixC)합니다.


* * *

<a id="Summary"></a>
## <a name="summary"></a>요약

이 랩에서 새로운 ASP.NET Web API 프레임 워크를 구현 프레임 워크를 사용 하는 RESTful 웹 api를 소개 했습니다. 여기에서 만들고 하는 임의 개수의 메커니즘을 사용 하 여 데이터 유지를 용이 하 게 하는 새 저장소 간단한 것이 랩에서 예로서 제공 하는 대신 해당 서비스를 연결 합니다. Web API에는 다양 한 HTTP 및 JSON 또는 XML을 지 원하는 모든 언어로 작성 된 HTML이 아닌 클라이언트 로부터의 통신을 설정 하는 등의 추가 기능을 지원 합니다. 일반 웹 응용 프로그램 외부의 웹 API를 호스트 하는 기능 또한으로 사용자 고유의 serialization 형식을 만드는 하는 기능.

ASP.NET 웹 사이트에 ASP.NET Web API 프레임 워크에서 전용 영역 [ [ https://asp.net/web-api ](https://asp.net/web-api) ](https://asp.net/web-api)합니다. 이 사이트를 계속 최신 정보, 샘플 및 웹 API와 관련 된 뉴스 있으므로 체크 자주 제공할 거의 모든 장치 또는 개발 프레임 워크를 사용할 수 있는 사용자 지정 웹 Api를 만드는 아트를 철저히 하려는 경우.

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a>부록 a: 코드 조각을 사용 하 여

코드 조각 바로 쉽게 얻습니다 필요한 코드를 수 있습니다. 랩 문서는 알려 정확 하 게 사용 가능 시기, 다음 그림에 나와 있는 것 처럼 합니다.

![Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여](build-restful-apis-with-aspnet-web-api/_static/image28.png "Visual Studio를 사용 하 여 코드 조각을 프로젝트에 코드를 삽입 하려면")

*Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여*

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a>키보드 (C#만)를 사용 하 여 코드 조각을 추가 하려면

1. 코드를 삽입 하려는 위치에 커서를 놓습니다.
2. 공백 또는 하이픈만) (없이 코드 조각 이름을 입력 하기 시작 합니다.
3. IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.
4. 올바른 코드 조각 선택 (또는 전체 코드 조각이 이름이 선택 될 때까지 입력 유지).
5. 커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.

    ![코드 조각 이름을 입력 하기 시작](build-restful-apis-with-aspnet-web-api/_static/image29.png "조각 이름을 입력 하기 시작")

    *코드 조각 이름을 입력 하기 시작*

    ![Tab 키를 눌러 강조 표시 된 코드 조각 선택](build-restful-apis-with-aspnet-web-api/_static/image30.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")

    *Tab 키를 눌러 강조 표시 된 코드 조각 선택*

    ![확장 하 고 Tab 키를 눌러 다시 코드 조각](build-restful-apis-with-aspnet-web-api/_static/image31.png "확장 하 고 Tab 키를 눌러 다시 코드 조각")

    *확장 하 고 Tab 키를 눌러 다시 코드 조각*

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a>마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면

1. 코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.
2. 선택 **조각 삽입** 이어서 **내 코드 조각**합니다.
3. 클릭 하 여 목록에서 관련 조각을 선택 합니다.

    ![코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭](build-restful-apis-with-aspnet-web-api/_static/image32.png "코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추 클릭")

    *코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭*

    ![클릭 하 여 목록에서 관련 조각을 선택](build-restful-apis-with-aspnet-web-api/_static/image33.png "클릭 하 여 목록에서 관련 조각을 선택")

    *클릭 하 여 목록에서 관련 조각을 선택합니다*

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a>부록 b: 설치 Visual Studio Express 2012 for Web

설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 버전을 사용 하 여 **[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)**. 다음 지침을 설치 하는 데 필요한 단계를 안내 하 *Visual studio Express 2012 for Web* 를 사용 하 여 *Microsoft 웹 플랫폼 설치 관리자*합니다.

1. 로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다. 또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Web Azure SDK와</em>&quot;합니다.
2. 클릭 **지금 설치**합니다. 없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.
3. 한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.

    ![Visual Studio Express 설치](build-restful-apis-with-aspnet-web-api/_static/image34.png "Visual Studio Express 설치")

    *Visual Studio Express 설치*
4. 모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.

    ![사용 조건 동의](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    *설치 진행률*
6. 설치가 완료 되 면 클릭 **마침**합니다.

    ![설치 완료](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    *설치 완료*
7. 클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.
8. Visual Studio Express for Web을 열려면로 이동는 **시작** 화면를 쓰기 시작할 &quot; **VS Express**&quot;, 클릭는 **VS Express for Web** 바둑판식 배열입니다.

    ![웹 타일에 대 한 VS Express](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    *웹 타일에 대 한 VS Express*

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>부록 c: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

이 부록에서는 Azure 포털에서 새 웹 사이트를 만들고 Azure에서 제공 하는 웹 배포 게시 기능을 활용 하기 위해 랩에서 수행 하 여 가져온 응용 프로그램을 게시 하는 방법을 보여줍니다.

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a>작업 1-Azure 포털에서 새 웹 사이트 만들기

1. 이동 하 여 [Azure 관리 포털](https://manage.windowsazure.com/) 구독에 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.

    > [!NOTE]
    > Azure를 무료로 10 개 ASP.NET 웹 사이트를 호스트 하 고 트래픽이 증가 됨을 확장 한 다음 사용할 수 있습니다. 등록할 수 [여기](http://aka.ms/aspnet-hol-azure)합니다.

    ![Windows Azure 포털에 로그온](build-restful-apis-with-aspnet-web-api/_static/image39.png "Windows Azure 포털에 로그인")

    *포털에 로그인*
2. 클릭 **새로** 명령 모음에서 합니다.

    ![새 웹 사이트를 만드는](build-restful-apis-with-aspnet-web-api/_static/image40.png "새 웹 사이트 만들기")

    *새 웹 사이트 만들기*
3. 클릭 **계산** | **웹 사이트**합니다. 그런 다음 선택 **빠른 생성** 옵션입니다. 새 웹 사이트에 대 한 사용 가능한 URL을 입력 하 고 클릭 **웹 사이트 만들기**합니다.

    > [!NOTE]
    > Azure는 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트입니다. 빨리 만들기 옵션을 사용 하면 포털 외부에서 Azure로 완료 된 웹 응용 프로그램을 배포할 수 있습니다. 데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.

    ![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](build-restful-apis-with-aspnet-web-api/_static/image41.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")

    *빠른 생성을 사용 하 여 새 웹 사이트 만들기*
4. 새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.
5. 웹 사이트가 만들어지면 아래 링크를 클릭 하 고 **URL** 열입니다. 새 웹 사이트가 작동 하는지 확인 합니다.

    ![새 웹 사이트를 찾아](build-restful-apis-with-aspnet-web-api/_static/image42.png "새 웹 사이트를 검색 합니다.")

    *새 웹 사이트를 검색합니다.*

    ![실행 중인 웹 사이트](build-restful-apis-with-aspnet-web-api/_static/image43.png "실행 중인 웹 사이트")

    *실행 중인 웹 사이트*
6. 포털로 돌아가서 아래에서 웹 사이트의 이름을 클릭는 **이름** 관리 페이지를 표시 하는 열입니다.

    ![웹 사이트 관리 페이지 열기](build-restful-apis-with-aspnet-web-api/_static/image44.png "웹 사이트 관리 페이지 열기")

    *웹 사이트 관리 페이지 열기*
7. 에 **대시보드** 페이지의 **눈에 보는** 섹션에서 클릭는 **게시 프로필 다운로드** 링크 합니다.

    > [!NOTE]
    > *게시 프로필* 각각의 활성화 된 게시 방법에 대 한 Azure에 웹 응용 프로그램을 게시 하는 데 필요한 정보가 모두 포함 되어 있습니다. 게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열이 포함 되어 있습니다. **Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 읽는 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화 Azure에 웹 응용 프로그램을 게시 합니다.

    ![게시 프로필 다운로드 웹 사이트](build-restful-apis-with-aspnet-web-api/_static/image45.png "게시 프로필 다운로드 웹 사이트")

    *게시 프로필 다운로드 웹 사이트*
8. 알려진된 위치에 게시 프로필 파일을 다운로드 합니다. 더 이상이 연습에서는 Visual Studio에서 Azure로 웹 응용 프로그램을 게시 하려면이 파일을 사용 하는 방법을 표시 됩니다.

    ![게시 프로필 파일을 저장](build-restful-apis-with-aspnet-web-api/_static/image46.png "게시 프로필 저장")

    *게시 프로필 파일을 저장합니다.*

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>작업 2-데이터베이스 서버 구성

응용 프로그램에서 SQL Server를 활용 하는 경우 데이터베이스를 SQL 데이터베이스 서버 만들기 해야 합니다. SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 태스크를 건너뛸 수 있습니다.

1. 응용 프로그램 데이터베이스를 저장 하기 위해 SQL 데이터베이스 서버를 해야 합니다. Azure 관리 포털에 구독에서 SQL 데이터베이스 서버를 볼 수 있습니다 **Sql 데이터베이스** | **서버** | **서버대시보드**. 만든 서버 없는 경우 수행 하 여 만들 수 있습니다는 **추가** 명령 모음에서 단추입니다. 기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**, 다음 작업에 사용 됩니다. 만들지 마십시오 데이터베이스 아직 대로 이후 단계에서 생성 됩니다.

    ![SQL 데이터베이스 서버 대시보드](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL 데이터베이스 서버 대시보드")

    *SQL 데이터베이스 서버 대시보드*
2. 다음 태스크에서는 서버 목록에 사용자의 로컬 IP 주소를 포함 해야 이러한 이유로 Visual Studio에서 데이터베이스 연결을 테스트 **허용 IP 주소**합니다. 작업을 수행 하려면 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여넣습니다는 **시작 IP 주소** 및 **끝IP주소** 클릭 하 고 텍스트 상자는 ![add-client-ip-address-ok-button](build-restful-apis-with-aspnet-web-api/_static/image48.png) 단추입니다.

    ![클라이언트 IP 주소를 추가합니다.](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    *클라이언트 IP 주소를 추가합니다.*
3. 한 번는 **클라이언트 IP 주소** 허용된 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 하 여 변경 사항을 확인 합니다.

    ![변경 확인](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    *변경 확인*

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

1. ASP.NET MVC 4 솔루션으로 돌아갑니다. 에 **솔루션 탐색기**웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.

    ![응용 프로그램을 게시](build-restful-apis-with-aspnet-web-api/_static/image51.png "응용 프로그램을 게시")

    *웹 사이트를 게시*
2. 첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.

    ![게시 프로필 가져오기](build-restful-apis-with-aspnet-web-api/_static/image52.png "게시 프로필 가져오기")

    *게시 프로필 가져오기*
3. 클릭 **연결 확인**합니다. 유효성 검사가 완료 되 면 클릭 **다음**합니다.

    > [!NOTE]
    > 연결 유효성 검사 단추 옆에 표시 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.

    ![연결 유효성 검사](build-restful-apis-with-aspnet-web-api/_static/image53.png "연결 유효성 검사")

    *연결 유효성 검사*
4. 에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추 클릭 (즉, **DefaultConnection**).

    ![웹 배포 구성](build-restful-apis-with-aspnet-web-api/_static/image54.png "웹 배포 구성")

    *웹 배포 구성*
5. 다음과 같이 데이터베이스 연결을 구성 합니다.

   - 에 **서버 이름** SQL 데이터베이스 서버 URL 사용 하 여 입력 된 *tcp:* 접두사입니다.
   - **사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.
   - **암호** 서버 관리자 로그인 암호를 입력 합니다.
   - 예를 들어 새 데이터베이스 이름 입력: *MVC4SampleDB*합니다.

     ![대상 연결 문자열 구성](build-restful-apis-with-aspnet-web-api/_static/image55.png "대상 연결 문자열 구성")

     *대상 연결 문자열 구성*
6. 그런 다음 **확인**을 클릭합니다. 데이터베이스를 만들려는 대화 상자가 나타나면 **예**합니다.

    ![데이터베이스를 만드는](build-restful-apis-with-aspnet-web-api/_static/image56.png "데이터베이스 문자열 만들기")

    *데이터베이스를 만드는 중*
7. Windows azure에서 SQL 데이터베이스에 연결 하기 위해 사용할 연결 문자열은 기본 연결 텍스트 상자 내에서 표시 됩니다. **다음**을 클릭합니다.

    ![SQL 데이터베이스를 가리키는 연결 문자열](build-restful-apis-with-aspnet-web-api/_static/image57.png "SQL 데이터베이스를 가리키는 연결 문자열")

    *SQL 데이터베이스를 가리키는 연결 문자열*
8. 에 **미리 보기** 페이지 **게시**합니다.

    ![웹 응용 프로그램을 게시](build-restful-apis-with-aspnet-web-api/_static/image58.png "웹 응용 프로그램 게시")

    *웹 응용 프로그램 게시*
9. 게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.

    ![Windows Azure에 게시 된 응용 프로그램](build-restful-apis-with-aspnet-web-api/_static/image59.png "Windows Azure에 게시 된 응용 프로그램")

    *Azure에 게시 된 응용 프로그램*
