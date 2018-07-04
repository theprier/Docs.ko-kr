---
uid: aspnet/overview/owin-and-katana/owin-startup-class-detection
title: OWIN 시작 클래스 검색 | Microsoft Docs
author: Praburaj
description: 이 자습서에는 OWIN 시작 클래스는 로드를 구성 하는 방법을 보여 줍니다. OWIN에 대 한 자세한 내용은 참조는 프로젝트 Katana 개요. 이 자습서를 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: 08257f55-36f4-4e39-9c88-2a5602838c79
ms.technology: ''
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-startup-class-detection
msc.type: authoredcontent
ms.openlocfilehash: d7e18001cbbfc67397f32ace53d347acf49d7537
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388700"
---
<a name="owin-startup-class-detection"></a>OWIN 시작 클래스 검색
====================
하 여 [Praburaj Thiagarajan](https://github.com/Praburaj), [Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서에는 OWIN 시작 클래스는 로드를 구성 하는 방법을 보여 줍니다. OWIN에 대 한 자세한 내용은 참조 하세요. [는 프로젝트 Katana 개요](an-overview-of-project-katana.md)합니다. Rick anderson이 자습서가 작성 ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) ), Praburaj Thiagarajan 및 Howard Dierking ( [ @howard \_dierking](https://twitter.com/howard_dierking) ).
> 
> ## <a name="prerequisites"></a>전제 조건
> 
> [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)


## <a name="owin-startup-class-detection"></a>OWIN 시작 클래스 검색

 모든 OWIN 응용 프로그램에 시작 클래스가 응용 프로그램 파이프라인에 대 한 구성 요소를 지정 하는 위치입니다. 여러 가지 방법으로 런타임에 startup 클래스를 연결할 수 있습니다, 호스팅 모델에 따라 있습니다 (OwinHost, IIS 및 IIS Express)을 선택 합니다. 이 자습서에 나와 있는 시작 클래스는 모든 호스팅 응용 프로그램에서 사용할 수 있습니다. 호스팅 런타임을 사용 하 여 다음 중 하나에 도달 startup 클래스를 연결 합니다.  

1. **명명 규칙**: Katana 라는 클래스를 찾고 `Startup` 어셈블리 이름 또는 전역 네임 스페이스를 일치 하는 네임 스페이스에 있습니다.
2. **OwinStartup 특성**:이 모드는 대부분의 개발자 startup 클래스를 지정 하는 데 걸리는 방법입니다. 다음 특성은으로 startup 클래스를 설정 합니다 `TestStartup` 클래스는 `StartupDemo` 네임 스페이스입니다. 

    [!code-csharp[Main](owin-startup-class-detection/samples/sample1.cs)]

   `OwinStartup` 특성 명명 규칙을 재정의 합니다. 이 특성을 사용 하 여 이름을 지정할 수도 있습니다, 있지만 이름을 사용 하도 사용 해야는 `appSetting` 구성 파일의 요소입니다.
3. **구성 파일에서 appSetting 요소**: 합니다 `appSetting` 재정의 `OwinStartup` 특성 및 명명 규칙. 여러 시작 클래스를 할 수 있습니다 (사용 하 여 각는 `OwinStartup` 특성) 및 startup 클래스는 다음과 유사한 태그를 사용 하 여 구성 파일에서 로드할 구성:  

    [!code-xml[Main](owin-startup-class-detection/samples/sample2.xml)]

   또한 startup 클래스 및 어셈블리를 명시적으로 지정 하는 다음 키를 사용할 수 있습니다. 

    [!code-xml[Main](owin-startup-class-detection/samples/sample3.xml)]

   구성 파일에 다음 XML의 친숙 한 시작 클래스 이름을 지정 `ProductionConfiguration`합니다.  

    [!code-xml[Main](owin-startup-class-detection/samples/sample4.xml)]

   위의 태그는 다음을 사용 하 여 사용 해야 합니다 `OwinStartup` 친숙 한 이름을 지정 하면 특성의 `ProductionStartup2` 클래스를 실행 합니다.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample5.cs?highlight=1,16)]
4. OWIN 시작 검색 추가 사용 하지 않도록 설정 합니다 `appSetting owin:AutomaticAppStartup` 값을 사용 하 여 `"false"` web.config 파일에서 합니다.

    [!code-xml[Main](owin-startup-class-detection/samples/sample6.xml)]

## <a name="create-an-aspnet-web-app-using-owin-startup"></a>OWIN 시작을 사용 하 여 ASP.NET 웹 앱 만들기

1. 빈 Asp.Net 웹 응용 프로그램을 만들고 이름을 **StartupDemo**합니다. -설치 `Microsoft.Owin.Host.SystemWeb` NuGet 패키지 관리자를 사용 하 여 합니다. **도구** 메뉴에서 **라이브러리 패키지 관리자**를 차례로 **패키지 관리자 콘솔**합니다. 다음 명령을 입력합니다.  

    [!code-powershell[Main](owin-startup-class-detection/samples/sample7.ps1)]
2. OWIN 시작 클래스를 추가 합니다. 선택한 Visual Studio 2013에서 프로젝트를 클릭 마우스 오른쪽 단추로 **클래스 추가**합니다.-합니다 **새 항목 추가** 대화 상자에 입력 *OWIN* 검색 필드에 이름 Startup.cs로 변경 클릭 하 고 **추가**합니다.  
  
     ![](owin-startup-class-detection/_static/image1.png)   
  
   추가 하려면 다음에 *Owin Startup 클래스*, 될에서 사용할 수 있는 합니다 **추가** 메뉴.  
   
     ![](owin-startup-class-detection/_static/image2.png)  
  
   또는 프로젝트를 마우스 오른쪽 단추로 클릭 수를 선택 **추가**을 선택한 후 **새 항목**를 선택한 후는 **Owin Startup 클래스**합니다.  
  
     ![](owin-startup-class-detection/_static/image3.png)  
  
- 생성된 된 코드를 대체 합니다 *Startup.cs* 다음 파일:  

    [!code-csharp[Main](owin-startup-class-detection/samples/sample8.cs?highlight=5,7,15-28,31-34)]
  
  `app.Use` 람다 식은 OWIN 파이프라인에 지정 된 미들웨어 구성 요소를 등록 하는 데 사용 됩니다. 이 경우 들어오는 요청에 응답 하기 전에 들어오는 요청 로깅을 설정 하는 합니다. 합니다 `next` 매개 변수는 대리자 ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt; [태스크](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx) &gt; ) 파이프라인의 다음 구성 요소입니다. `app.Run` 람다 식 들어오는 요청에 파이프라인 후크 및 응답 메커니즘을 제공 합니다.
     > [!NOTE]
     > 위의 코드에서 우리는 주석으로 처리를 `OwinStartup` 특성과 것 이라는 클래스를 실행 하는 규칙에 의존 하는 `Startup` 합니다.-키를 눌러 ***F5*** 응용 프로그램을 실행 합니다. 몇 번 새로 고침을 누릅니다.  
  
    ![](owin-startup-class-detection/_static/image4.png)  
  이 자습서에서는 이미지에 표시 된 숫자 참고: 참조 수가 일치 하지 않습니다. 밀리초 문자열 페이지를 새로 고칠 때 새 응답이 표시 됩니다.  
  추적 정보를 볼 수는 **출력** 창입니다.  
  
    ![](owin-startup-class-detection/_static/image5.png)

## <a name="add-more-startup-classes"></a>자세한 시작 클래스 추가

이 단원의 다른 시작 클래스를 추가 하겠습니다. 응용 프로그램에 여러 OWIN 시작 클래스를 추가할 수 있습니다. 예를 들어, 다음 개발, 테스트 및 프로덕션에 대 한 시작 클래스를 만들 수는 것이 좋습니다.

1. 새 OWIN 시작 클래스를 만들고 이름을 `ProductionStartup`입니다.
2. 생성된 코드를 다음으로 바꿉니다.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample9.cs?highlight=14-18)]
3. 컨트롤 F5 키를 눌러 앱을 실행 합니다. `OwinStartup` 프로덕션 startup 클래스를 실행 하는 특성을 지정 합니다.  
  
    ![](owin-startup-class-detection/_static/image6.png)
4. 다른 OWIN Startup 클래스를 만들고 이름을 `TestStartup`입니다.
5. 생성된 코드를 다음으로 바꿉니다.  

    [!code-csharp[Main](owin-startup-class-detection/samples/sample10.cs?highlight=6,14-18)]

   합니다 `OwinStartup` 위의 특성 오버 로드는 지정 `TestingConfiguration` 으로 *친숙 한* Startup 클래스의 이름입니다.
6. 열기는 *web.config* 파일과 Startup 클래스의 이름을 지정 하는 OWIN 앱 시작 키를 추가 합니다.

    [!code-xml[Main](owin-startup-class-detection/samples/sample11.xml?highlight=3-5)]
7. 컨트롤 F5 키를 눌러 앱을 실행 합니다. 앱 설정 요소가 참조 하는 셀을 취하고 테스트 구성을 실행 하는 합니다.  
  
    ![](owin-startup-class-detection/_static/image7.png)
8. 제거는 *친숙 한* 이름을 합니다 `OwinStartup` 특성을 `TestStartup` 클래스.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample12.cs)]
9. 에 OWIN 앱 시작 키를 대체 합니다 *web.config* 다음 파일:

    [!code-xml[Main](owin-startup-class-detection/samples/sample13.xml)]
10. 되돌리기는 `OwinStartup` Visual Studio에서 생성 된 기본 특성 코드에 각 클래스에 있는 특성:  

    [!code-csharp[Main](owin-startup-class-detection/samples/sample14.cs)]

    각 OWIN 앱 시작 키 아래 프로덕션 클래스를 실행 하면 됩니다. 

    [!code-xml[Main](owin-startup-class-detection/samples/sample15.xml)]

    마지막 시작 키 시작 구성 메서드를 지정합니다. 다음 OWIN 앱 시작 키를 사용 하면 구성 클래스의 이름을 변경 하려면 `MyConfiguration` 합니다.

    [!code-xml[Main](owin-startup-class-detection/samples/sample16.xml)]

## <a name="using-owinhostexe"></a>Owinhost.exe를 사용 하 여

1. 다음 태그를 사용 하 여 Web.config 파일을 바꿉니다.  

    [!code-xml[Main](owin-startup-class-detection/samples/sample17.xml?highlight=3-6)]

   이 경우이 마지막 키 wins `TestStartup` 지정 됩니다.
2. PMC에서 Owinhost를 설치 합니다. 

    [!code-console[Main](owin-startup-class-detection/samples/sample18.cmd)]
3. 응용 프로그램 폴더로 이동 (포함 된 폴더를 *Web.config* 파일) 및 명령 프롬프트 및 종류: 

    [!code-console[Main](owin-startup-class-detection/samples/sample19.cmd)]

   명령 창에 표시 됩니다. 

    [!code-console[Main](owin-startup-class-detection/samples/sample20.cmd)]
4. URL로 브라우저 시작 `http://localhost:5000/`합니다.  
  
    ![](owin-startup-class-detection/_static/image8.png)  
  
   OwinHost 위에 나열 된 시작 규칙을 적용 합니다.
5. 명령 창에서 enter 키를 눌러 OwinHost를 종료 합니다.
6. 에 `ProductionStartup` 클래스의 이름을 지정 하는 다음 OwinStartup 특성을 추가 합니다 *ProductionConfiguration*합니다.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample21.cs)]
7. 명령 프롬프트 및 형식: 

    [!code-console[Main](owin-startup-class-detection/samples/sample22.cmd)]

   프로덕션 시작 클래스 로드 됩니다.  
    ![](owin-startup-class-detection/_static/image9.png)  
   응용 프로그램에 여러 시작 클래스 및이 예제에서는 시작 로드할 클래스를 런타임 시까지 지연 합니다.
8. 다음 런타임 시작 옵션을 테스트 합니다.

    [!code-console[Main](owin-startup-class-detection/samples/sample23.cmd)]
