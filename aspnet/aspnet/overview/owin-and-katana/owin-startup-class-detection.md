---
uid: aspnet/overview/owin-and-katana/owin-startup-class-detection
title: "OWIN 시작 클래스 검색 | Microsoft Docs"
author: Praburaj
description: "이 자습서에는 OWIN 시작 클래스 로드를 구성 하는 방법을 보여 줍니다. OWIN에 대 한 자세한 내용은 참조는 프로젝트 Katana 개요. 이 자습서가 되었습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: 08257f55-36f4-4e39-9c88-2a5602838c79
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-startup-class-detection
msc.type: authoredcontent
ms.openlocfilehash: 618f8fa23630dcf9821a54415766dc015694e535
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="owin-startup-class-detection"></a>OWIN 시작 클래스 검색
====================
여 [Praburaj Thiagarajan](https://github.com/Praburaj), [Rick Anderson](https://github.com/Rick-Anderson)

> 이 자습서에는 OWIN 시작 클래스 로드를 구성 하는 방법을 보여 줍니다. OWIN에 대 한 자세한 내용은 참조 하십시오. [An 프로젝트 Katana 개요](an-overview-of-project-katana.md)합니다. 이 자습서는 Rick Anderson에 의해 작성 되었으므로 ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) ), Praburaj Thiagarajan 및 Howard Dierking ( [ @howard \_dierking](https://twitter.com/howard_dierking) ).
> 
> ## <a name="prerequisites"></a>필수 구성 요소
> 
> [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)


## <a name="owin-startup-class-detection"></a>OWIN 시작 클래스 검색

 모든 OWIN 응용 프로그램에 응용 프로그램 파이프라인에 대 한 구성 요소를 지정 하는 시작 클래스입니다. 여러 가지 방법으로 런타임 시작 클래스를 연결할 수 있습니다, 호스팅 모델에 따라 있습니다 (예: OwinHost, IIS 및 IIS Express)을 선택 합니다. 이 자습서에 표시 된 시작 클래스입니다. 모든 호스팅 응용 프로그램에 사용할 수 있습니다. 호스팅 런타임을 사용 하 여 다음 중 하나에 도달한 시작 클래스를 연결:  

1. **명명 규칙**: Katana 라는 클래스를 찾고 `Startup` 어셈블리 이름 또는 전역 네임 스페이스와 일치 하는 네임 스페이스에 있습니다.
2. **OwinStartup 특성이**: 이것은 대부분의 개발자 시작 클래스를 지정 하는 데 걸리는 방식입니다. 다음 특성은 시작 클래스도 설정 된 `TestStartup` 클래스에 `StartupDemo` 네임 스페이스입니다. 

    [!code-csharp[Main](owin-startup-class-detection/samples/sample1.cs)]

 `OwinStartup` 특성 명명 규칙을 재정의 합니다. 그러나 친숙 한 이름을 사용 하 여도 사용 해야,이 특성으로 사용할 이름을 지정할 수도 있습니다는 `appSetting` 구성 파일의 요소입니다.
3. **구성 파일의 appSetting 요소**:는 `appSetting` 요소 재정의 `OwinStartup` 특성 및 명명 규칙입니다. 여러 개의 시작 클래스 (사용 하 여 각는 `OwinStartup` 특성) 하 고 다음과 유사한 태그를 사용 하 여 구성 파일에서 로드할 수 있는 시작 클래스를 구성 합니다.  

    [!code-xml[Main](owin-startup-class-detection/samples/sample2.xml)]

 또한 명시적으로 시작 클래스 및 어셈블리를 지정 하는 다음 키를 사용할 수 있습니다. 

    [!code-xml[Main](owin-startup-class-detection/samples/sample3.xml)]

 구성 파일에 다음 XML의 친숙 한 시작 클래스 이름을 지정 `ProductionConfiguration`합니다.  

    [!code-xml[Main](owin-startup-class-detection/samples/sample4.xml)]

 다음으로는 위의 태그를 사용 해야 합니다 `OwinStartup` 친숙 한 이름을 지정 하 고 발생 하는 특성의 `ProductionStartup2` 실행 하는 클래스입니다.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample5.cs?highlight=1,16)]
4. OWIN 시작 검색을 해제 하려면 추가 `appSetting owin:AutomaticAppStartup` 값 `"false"` web.config 파일에 있습니다.

    [!code-xml[Main](owin-startup-class-detection/samples/sample6.xml)]

## <a name="create-an-aspnet-web-app-using-owin-startup"></a>OWIN 시작을 사용 하 여 ASP.NET 웹 앱 만들기

1. 빈 Asp.Net 웹 응용 프로그램을 만들고 이름을 **StartupDemo**합니다. -설치 `Microsoft.Owin.Host.SystemWeb` NuGet 패키지 관리자를 사용 하 여 합니다. **도구** 메뉴 선택 **라이브러리 패키지 관리자**, 차례로 **패키지 관리자 콘솔**합니다. 다음 명령을 입력합니다.  

    [!code-powershell[Main](owin-startup-class-detection/samples/sample7.ps1)]
- OWIN 시작 클래스를 추가 합니다. Visual Studio 2013에서 마우스 오른쪽 단추로 클릭 하 여 프로젝트 및 선택 **클래스 추가**.-는 **새 항목 추가** 대화 상자에 입력 *OWIN* 검색 필드 및 이름 Startup.cs로 변경 클릭 하 고 **추가**합니다.  
  
    ![](owin-startup-class-detection/_static/image1.png)   
  
 추가 하려면 다음에 *Owin 시작 클래스*, 됩니다에서 사용할 수는 **추가** 메뉴.  
   
    ![](owin-startup-class-detection/_static/image2.png)  
  
 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택할 수 또는 **추가**을 선택한 후 **새 항목**를 선택한 후는 **Owin 시작 클래스**합니다.  
  
    ![](owin-startup-class-detection/_static/image3.png)  
  
- 생성 된 코드는 *Startup.cs* 다음 파일:  

    [!code-csharp[Main](owin-startup-class-detection/samples/sample8.cs?highlight=5,7,15-28,31-34)]
  
 `app.Use` 람다 식을 OWIN 파이프라인에 지정 된 미들웨어 구성 요소를 등록 하는 데 사용 됩니다. 이 경우 들어오는 요청에 응답 하기 전에 들어오는 요청의 로깅을 설정 하는 합니다. `next` 매개 변수는 대리자 ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt; [작업](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx) &gt; ) 파이프라인의 다음 구성 요소입니다. `app.Run` 람다 식을 연결 하는 들어오는 요청에 파이프라인 및 응답 메커니즘을 제공 합니다.
     > [!NOTE]
     > 위의 코드에서 우리는 주석으로 처리는 `OwinStartup` 특성과 우리 라는 클래스를 실행 중인 규칙을 사용 하 `Startup` .-키를 눌러 ***F5*** 응용 프로그램을 실행 합니다. 여러 번 새로 고침을 누릅니다.  
  
    ![](owin-startup-class-detection/_static/image4.png)  
이 자습서에서는 이미지에 표시 된 숫자 참고: 참조 수가 일치 하지 않습니다. 밀리초 문자열이 페이지를 새로 고칠 때 새 응답을 표시 하도록 사용 됩니다.  
 추적 정보를 볼 수는 **출력** 창.  
  
    ![](owin-startup-class-detection/_static/image5.png)

## <a name="add-more-startup-classes"></a>더 많은 시작 클래스 추가

이 섹션의 시작 클래스를 하나 더 추가 합니다. OWIN 시작 클래스를 여러 응용 프로그램에 추가할 수 있습니다. 예를 들어, 개발, 테스트 및 프로덕션에 대 한 시작 클래스를 만들 수도 있습니다.

1. OWIN 시작 새 클래스를 만들고 이름을 `ProductionStartup`합니다.
2. 생성된 코드를 다음으로 바꿉니다.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample9.cs?highlight=14-18)]
3. F5 컨트롤을 응용 프로그램을 실행 합니다. `OwinStartup` 특성 프로덕션 시작 클래스입니다.이 실행을 지정 합니다.  
  
    ![](owin-startup-class-detection/_static/image6.png)
4. OWIN 시작 클래스를 하나 더 만들고 이름을 `TestStartup`합니다.
5. 생성된 코드를 다음으로 바꿉니다.  

    [!code-csharp[Main](owin-startup-class-detection/samples/sample10.cs?highlight=6,14-18)]

 `OwinStartup` 위의 오버 로드는 특성 지정 `TestingConfiguration` 로 *친숙 한* 시작 클래스의 이름입니다.
6. 열기는 *web.config* 파일을 시작 클래스의 이름을 지정 하는 OWIN 응용 프로그램 시작 키를 추가 합니다.

    [!code-xml[Main](owin-startup-class-detection/samples/sample11.xml?highlight=3-5)]
7. F5 컨트롤을 응용 프로그램을 실행 합니다. 앱 설정 요소의 참조 하는 셀을 취하고 테스트 구성이 실행 합니다.  
  
    ![](owin-startup-class-detection/_static/image7.png)
8. 제거는 *친숙 한* 에서 이름는 `OwinStartup` 특성에 `TestStartup` 클래스입니다.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample12.cs)]
9. 에 OWIN 응용 프로그램 시작 키를 교체는 *web.config* 다음 파일:

    [!code-xml[Main](owin-startup-class-detection/samples/sample13.xml)]
10. 되돌리기는 `OwinStartup` Visual Studio에서 생성 된 기본 특성 코드에 각 클래스에 특성:  

    [!code-csharp[Main](owin-startup-class-detection/samples/sample14.cs)]

 아래 OWIN 응용 프로그램 시작 키를 각각은 프로덕션 클래스를 실행 하면 됩니다. 

    [!code-xml[Main](owin-startup-class-detection/samples/sample15.xml)]

 마지막 시작 키 시작 구성 방법을 지정합니다. 다음 OWIN 응용 프로그램 시작 키를 사용 하면 구성 클래스의 이름을 변경 하려면 `MyConfiguration` 합니다.

    [!code-xml[Main](owin-startup-class-detection/samples/sample16.xml)]

## <a name="using-owinhostexe"></a>Owinhost.exe를 사용 하 여

1. Web.config 파일을 다음 태그로 바꿉니다.  

    [!code-xml[Main](owin-startup-class-detection/samples/sample17.xml?highlight=3-6)]

 따라서이 경우 마지막 키 wins `TestStartup` 지정 됩니다.
2. PMC Owinhost를 설치 합니다. 

    [!code-console[Main](owin-startup-class-detection/samples/sample18.cmd)]
3. 응용 프로그램 폴더를 찾습니다 (포함 하는 폴더는 *Web.config* 파일) 및 유형과 명령 프롬프트에서: 

    [!code-console[Main](owin-startup-class-detection/samples/sample19.cmd)]

 명령 창이 표시 됩니다. 

    [!code-console[Main](owin-startup-class-detection/samples/sample20.cmd)]
4. URL로 브라우저 시작 `http://localhost:5000/`합니다.  
  
    ![](owin-startup-class-detection/_static/image8.png)  
  
 OwinHost 위에 나열 된 시작 규칙을 적용 합니다.
5. 명령 창에서 enter 키를 눌러 OwinHost를 종료 합니다.
6. 에 `ProductionStartup` 클래스의 이름을 지정 하는 다음 OwinStartup 특성을 추가, *ProductionConfiguration*합니다.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample21.cs)]
7. 명령 프롬프트 및 형식: 

    [!code-console[Main](owin-startup-class-detection/samples/sample22.cmd)]

 프로덕션 시작 클래스 로드 됩니다.  
    ![](owin-startup-class-detection/_static/image9.png)  
 응용 프로그램에 여러 시작 클래스가 하며이 예제에서는 시작 로드할 클래스를 런타임까지 지연 합니다.
8. 다음과 같은 런타임 시작 옵션을 테스트 합니다.

    [!code-console[Main](owin-startup-class-detection/samples/sample23.cmd)]
