---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: "ASP.NET MVC 4 종속성 주입 | Microsoft Docs"
author: rick-anderson
description: "참고:이 실습 랩 ASP.NET MVC 4 및 ASP.NET MVC 필터에 대 한 기본 지식이 있다고 가정 합니다. ASP.NET MVC 4 필터 하기 전에 사용 하지 않은 rec... 하는 경우"
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: c735bbdafe4b8f0423abb6bacd076f173a1be9d8
ms.sourcegitcommit: 7ac15eaae20b6d70e65f3650af050a7880115cbf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="aspnet-mvc-4-dependency-injection"></a>ASP.NET MVC 4 종속성 주입

으로 [웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트를 다운로드 합니다.](https://aka.ms/webcamps-training-kit)

이 실습 랩 대 한 기본 지식이 있다고 가정 하 고 **ASP.NET MVC** 및 **필터링 하는 ASP.NET MVC 4**합니다. 사용 하지 않은 경우 **필터링 하는 ASP.NET MVC 4** 를 권장 앞, **ASP.NET MVC 사용자 지정 작업 필터** 실습 랩입니다.

> [!NOTE]
> 모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다. 이 랩에 특정 프로젝트에서 사용할 수는 [ASP.NET MVC 4 종속성 주입](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection)합니다.

**개체 지향 프로그래밍** 패러다임을 개체가 함께 동작 하는 공동 작업 모델에 없는 다음 참가자와 소비자입니다. 당연히이 통신 모델 개체 및 복잡성이 증가 하는 경우 관리 하기 어려운 되 고 구성 요소 간의 종속성을 생성 합니다.

![종속성 클래스 및 복잡성을 모델링](aspnet-mvc-4-dependency-injection/_static/image1.png "종속성 클래스 및 복잡성을 모델링")

*모델의 복잡성 및 클래스 종속성*

에 대 한 들어보았을는 **팩터리 패턴** 및 인터페이스와 서비스를 사용 하 여 클라이언트 개체가 서비스 위치에 대 한 책임 많습니다 구현 간의 분리 합니다.

종속성 주입 패턴은 Inversion of Control의 특정 구현 합니다. **(IoC) 제어** 개체 정상적인 작업 수행에 기초가 되는 다른 개체를 만들지 않는 것을 의미 합니다. 대신, (예를 들어 xml 구성 파일)를 외부 소스에서 필요한 개체를 가져올 있습니다.

**DI (dependency Injection)** 은 있음을 나타내고이 수행한 개체 개입 없이 일반적으로 생성자 매개 변수를 전달 하는 프레임 워크 구성 요소 속성을 설정 합니다.

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a>종속성 주입 (DI) 디자인 패턴

종속성 주입의 목표는 하는 상위 수준에서 클라이언트 클래스 (예: *는 골퍼*) 필요한 인터페이스를 충족 하는 항목 (예: *IClub*). 구체적인 유형 이란 신경 쓰지 않습니다 (예: *WoodClub, IronClub, WedgeClub* 또는 *PutterClub*), 부에서는 문제를 해결 하려면 다른 사용자 (좋은 예: *caddy*). ASP.NET MVC의 종속성 확인자를 사용 하면 종속성 논리를 다른 곳에 등록할 수 있습니다 (예: 컨테이너 또는 *클럽 모음*).

![종속성 주입 다이어그램](aspnet-mvc-4-dependency-injection/_static/image2.png "종속성 주입 그림")

*종속성 주입-골프 유추*

종속성 주입 패턴 및 Inversion of Control을 사용 하는 이점은 다음과 같습니다.

- 클래스 결합을 감소
- 코드 다시 사용 증가
- 코드 유지 관리를 향상 시킵니다.
- 응용 프로그램 테스트 향상 됩니다.

> [!NOTE]
> 종속성 주입은 경우에 따라 추상 팩터리 디자인 패턴을 비교 하 하지만 두 방법 모두 간에 약간의 차이가 없습니다. DI는 팩터리는 및에서 등록 된 서비스를 호출 하 여 종속성을 해결 하기 위해 뒤에서 작업 하는 프레임 워크를 있습니다.


종속성 주입 패턴 이해 했으므로 배웁니다이 랩을 통해 ASP.NET MVC 4의 적용 하는 방법. 종속성 주입을 사용 하 여 먼저는 **컨트롤러** 데이터베이스 액세스 서비스를 포함 하도록 합니다. 종속성 주입을 적용 하는 다음으로 **뷰** 서비스를 사용 하 여 정보를 표시 합니다. 마지막으로 확장 합니다는 DI ASP.NET MVC 4 필터를 솔루션에 사용자 지정 작업 필터를 삽입 합니다.

이 실습 랩에서 배우게 됩니다 하는 방법:

- NuGet 패키지를 사용 하 여 종속성 주입을 위한 ASP.NET MVC 4 Unity와 통합
- ASP.NET MVC 컨트롤러 내의 종속성 주입을 사용 하 여
- ASP.NET MVC 뷰 내 종속성 주입을 사용 하 여
- ASP.NET MVC 작업 필터 내부 종속성 주입을 사용 하 여

> [!NOTE]
> 이 랩에서 Unity.Mvc3 NuGet 패키지를 사용 하는 종속성 확인에 대 한 하지만 ASP.NET MVC 4를 사용 하는 종속성 주입 프레임 워크에 맞게 가능 합니다.


<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>필수 구성 요소

이 랩을 완료 하려면 다음 항목이 있어야 합니다.

- [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽기 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>설정

**설치 하는 코드 조각**

편의 위해는이 랩에 따라 관리 코드의 대부분 Visual Studio 코드 조각 수 있습니다. 실행 코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.

이 문서에서 부록을 참조할 수 사용 하는 방법에 알아봅니다 사용 하 고 Visual Studio 코드 조각에 익숙한 경우 &quot; [부록 b:를 사용 하 여 코드 조각을](#AppendixB)&quot;합니다.

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>연습

이 실습 랩에서 다음 연습으로 구성 됩니다.

1. [연습 1: 한 컨트롤러를 삽입합니다.](#Exercise1)
2. [연습 2: 뷰를 삽입합니다.](#Exercise2)
3. [연습 3: 필터를 삽입합니다.](#Exercise3)

> [!NOTE]
> 각 연습 동반 되는 **끝** 연습을 완료 한 후 가져와야 생성 되는 솔루션에 포함 된 폴더입니다. 연습을 통해 작업 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.


예상 소요 시간: **30 분**합니다.

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a>연습 1: 한 컨트롤러를 삽입합니다.

이 연습에서는 NuGet 패키지를 사용 하 여 Unity를 통합 하 여 ASP.NET MVC 컨트롤러의 종속성 주입을 사용 하는 방법에 설명 합니다. 이러한 이유로, 데이터 액세스에서 논리를 분리 하 여 MvcMusicStore 컨트롤러에 서비스를 포함 합니다. 서비스의 도움을 받아 종속성 주입을 사용 하 여 확인 될 컨트롤러 생성자에서 새 종속성이 생성 됩니다 **Unity**합니다.

이 방법은 덜 결합 하는 응용 프로그램은 보다 유연 하 고 쉽게 유지 관리 및 테스트를 생성 하는 방법을 설명 합니다. 또한 ASP.NET MVC Unity와 통합 하는 방법을 배웁니다.

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a>StoreManager 서비스에 대 한

라는 저장소 컨트롤러 데이터를 관리 하는 서비스를 포함 하는 이제 begin 솔루션에서 제공 하는 MVC Music Store **StoreService**합니다. 다음 저장소 서비스 구현을 찾을 수 있습니다. 참고 메서드를 모두 모델 엔터티를 반환 합니다.

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

**StoreController** 는 begin에서 솔루션 이제 소비 **StoreService**합니다. 모든 데이터 참조에서 제거 된 **StoreController**, 및 현재 데이터 액세스 공급자를 사용 하는 모든 방법을 변경 하지 않고 수정 하는 현재 사용 가능한 **StoreService**합니다.

아래에 있습니다는 **StoreController** 구현 인 종속성에 **StoreService** 클래스 생성자 내부 합니다.

> [!NOTE]
> 이 연습에 도입 된 종속성은 관련이 **Inversion of Control** (IoC).
> 
> **StoreController** 클래스 생성자 수신는 **IStoreService** 클래스 내에서 서비스를 호출을 수행 하는 데 필수적인 형식 매개 변수입니다. 그러나 **StoreController** 모든 컨트롤러는 ASP.NET MVC와 함께 작동 하도록 되어 있어야 합니다 (매개 변수 없이)와 기본 생성자를 구현 하지 않습니다.
> 
> 종속성을 해결 하려면 (지정 된 형식의 모든 개체를 반환 하는 클래스)는 추상 팩터리에서 생성 하는 컨트롤러에 있습니다.


[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> 클래스 선언 된 매개 변수가 없는 생성자가 없습니다 그대로 서비스 개체를 전송 하지 않고는 StoreController 만들려고 시도 하는 경우 오류를 받습니다.


<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a>작업 1-응용 프로그램 실행

이 태스크에서는 응용 프로그램 논리에서 데이터 액세스를 구분 하는 저장소 컨트롤러에 서비스를 포함 하는 Begin 응용 프로그램을 실행 합니다.

응용 프로그램을 실행할 때 컨트롤러 서비스가 기본적으로 매개 변수로 전달 하지 때 예외가 표시 됩니다.

1. 열기는 **시작** 솔루션에 있는 **Source\Ex01 주입 Controller\Begin**합니다.

    1. 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 전에 계속 합니다. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
    2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
    3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

    > [!NOTE]
    > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 키를 눌러 **Ctrl + f 5를 눌러** 디버깅 하지 않고 응용 프로그램을 실행 합니다. 오류 메시지를 받아볼 수 &quot; **이 개체에 대해 정의 된 매개 변수가 없는 생성자가 없습니다**&quot;:

    ![ASP.NET MVC 시작 응용 프로그램을 실행 하는 동안 오류가 발생 했습니다](aspnet-mvc-4-dependency-injection/_static/image3.png "ASP.NET MVC 시작 응용 프로그램을 실행 하는 동안 오류가 발생 했습니다")

    *ASP.NET MVC 시작 응용 프로그램을 실행 하는 동안 오류가 발생 했습니다*
3. 브라우저를 닫습니다.

다음 단계에서 음악 스토어 솔루션이 컨트롤러에서 필요로 하는 종속성 주입을 사용 합니다.

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a>작업 2-MvcMusicStore 솔루션에 포함 하 여 Unity

이 작업에서는 포함 됩니다 **Unity.Mvc3** NuGet 패키지를 솔루션입니다.

> [!NOTE]
> Unity.Mvc3 패키지는 ASP.NET MVC 3 용 하는데 ASP.NET MVC 4 완벽 하 게 호환 됩니다.
> 
> Unity 인스턴스에 대 한 선택적으로 지원 하 고 확장 가능한 경량 종속성 주입 컨테이너는 하 고 인터 셉 션을 입력 합니다. 그는 모든 유형의.NET 응용 프로그램에서 사용 하기 위해 범용 컨테이너입니다. 포함 하는 종속성 주입 메커니즘에 모든 일반적인 기능을 제공: 개체 만들기, 컨테이너에 구성 요소 구성을 연기 하 여 런타임 및 유연성을에서 종속성을 지정 하 여 요구 사항의 추상화 합니다.


1. 설치 **Unity.Mvc3** 에서 NuGet 패키지는 **MvcMusicStore** 프로젝트. 이 작업을 수행 하려면 엽니다는 **패키지 관리자 콘솔** 에서 **보기** | **다른 창**합니다.
2. 다음 명령을 실행합니다.

    PMC

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    ![Unity.Mvc3 NuGet 패키지 설치](aspnet-mvc-4-dependency-injection/_static/image4.png "Unity.Mvc3 NuGet 패키지 설치")

    *Unity.Mvc3 NuGet 패키지 설치*
3. 한 번의 **Unity.Mvc3** 패키지를 설치, 파일 및 Unity 구성을 단순화 하기 위해 자동으로 추가 하는 폴더를 탐색 합니다.

    ![Unity.Mvc3 패키지가 설치](aspnet-mvc-4-dependency-injection/_static/image5.png "Unity.Mvc3 패키지 설치")

    *Unity.Mvc3 패키지 설치*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-applicationstart"></a>작업 3-Global.asax.cs 응용 프로그램에서 등록 Unity\_시작

이 태스크에서는 업데이트 됩니다는 **응용 프로그램\_시작** 메서드에 있는 **Global.asax.cs** Unity 부트스트래퍼 이니셜라이저를 호출 하 고 그런 다음 부트스트래퍼 파일 등록을 업데이트 하려면 서비스와 컨트롤러에는 종속성 주입을 사용 합니다.

1. 이제 Unity 컨테이너를 초기화 하는 파일인 부트스트래퍼 및 종속성 확인자를 후크 할 수 있습니다. 이 위해 열고 **Global.asax.cs** 내에서 강조 표시 된 다음 코드를 추가 하 고는 **응용 프로그램\_시작** 메서드.

    (코드 조각- *ASP.NET 종속성 주입 랩-Ex01-Unity 초기화*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. 열기 **Bootstrapper.cs** 파일입니다.
3. 네임 스페이스를 포함: **MvcMusicStore.Services** 및 **MusicStore.Controllers**합니다.

    (코드 조각- *ASP.NET 종속성 주입-Ex01-랩 부트스트래퍼 네임 스페이스 추가*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. 대체 **BuildUnityContainer** 메서드의 저장소 컨트롤러 및 저장소 서비스를 등록 하는 다음 코드를 사용 하 여 콘텐츠입니다.

    (코드 조각- *ASP.NET 종속성 주입-Ex01-랩 레지스터 저장소 컨트롤러와 서비스*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>작업 4-응용 프로그램 실행

이 태스크에서는 해당 로드할 수 있는지 이제 Unity를 포함 한 후 확인 하려면 응용 프로그램을 실행 합니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 하려면 응용 프로그램이 모든 오류 메시지를 표시 하지 않고 로드 이제 해야 합니다.

    ![종속성 주입 된 응용 프로그램을 실행](aspnet-mvc-4-dependency-injection/_static/image6.png "종속성 주입 된 응용 프로그램을 실행 합니다.")

    *종속성 주입 된 응용 프로그램을 실행합니다.*
2. 찾아 **/저장소**합니다. 이렇게 하면 **StoreController**를 사용 하 여 이제 만들어지는 **Unity**합니다.

    ![MVC Music Store](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC Music Store")

    *MVC Music Store*
3. 브라우저를 닫습니다.

다음 연습에서는 ASP.NET MVC 뷰 및 작업 필터 내 사용 하는 종속성 주입 범위를 확장 하는 방법에 설명 합니다.

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a>연습 2: 뷰를 삽입합니다.

이 연습에서는 ASP.NET MVC 4의 새로운 기능으로 보기에서 Unity 통합에 대 한 종속성 주입을 사용 하는 방법에 설명 합니다. 파일을 수집 하려면 메시지와 아래 이미지를 보여 주는 저장소 찾아보기 보기 내에서 사용자 지정 서비스를 호출 합니다.

그런 다음 프로젝트를 Unity로 통합를 종속성 삽입 하는 사용자 지정 종속성 확인자를 만듭니다.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a>작업 1-서비스를 사용 하는 보기를 만드는 방법

이 태스크에서는 새 종속성을 생성 하는 서비스 호출을 수행 하는 뷰를 만듭니다. 이 솔루션에 포함 된 간단한 메시징 서비스에서 서비스 구성 됩니다.

1. 열기는 **시작** 솔루션에 있는 **Source\Ex02 주입 View\Begin** 폴더입니다. 그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.

    1. 제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
    2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
    3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

    > [!NOTE]
    > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
    > 
    > 자세한 내용은이 문서를 참조 하십시오.: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)합니다.
2. 포함 된 **MessageService.cs** 및 **IMessageService.cs** 클래스에 배치는 **\Assets 원본** 폴더에 **/서비스**합니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 **서비스** 폴더와 선택 **기존 항목 추가**합니다. 파일의 위치를 찾아를 포함 합니다.

    ![메시지 서비스 및 서비스 인터페이스 추가](aspnet-mvc-4-dependency-injection/_static/image8.png "메시지 서비스 및 서비스 인터페이스 추가")

    *추가 메시지 서비스 및 서비스 인터페이스*

    > [!NOTE]
    > **IMessageService** 인터페이스에 의해 구현 되는 두 개의 속성을 정의 합니다.는 **MessageService** 클래스입니다. 이러한 속성-**메시지** 및 **ImageUrl**-표시 되는 메시지와 이미지의 URL을 저장 합니다.
3. 폴더 만들기 **페이지/** 프로젝트의 루트 폴더를 한 다음 기존 클래스를 추가 **MyBasePage.cs** 에서 **Source\Assets**합니다. 상속 하는 기본 페이지는 다음과 같은 구조를 있습니다.

    ![페이지 폴더](aspnet-mvc-4-dependency-injection/_static/image9.png "페이지 폴더")

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. 열기 **Browse.cshtml** 에서 보려는 **/뷰/저장** 폴더에서 상속 하는 것을 확인 하 고 **MyBasePage.cs**합니다.

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. 에 **찾아보기** 보기에서 호출을 추가 **MessageService** 이미지 및 서비스에서 검색 메시지를 표시 하려면.
(C#)

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a>작업 2-사용자 지정 종속성 해결 프로그램 및 사용자 지정 뷰 페이지 활성기를 포함 하 여

이전 태스크에서 내부 서비스 호출을 수행 하는 뷰 내 새 종속성을 삽입 합니다. ASP.NET MVC 종속성 주입 인터페이스를 구현 하 여 해당 종속성을 확인 되는 이제 **IViewPageActivator** 및 **되며 IDependencyResolver**합니다. 구현 솔루션에 포함 됩니다 **되며 IDependencyResolver** Unity를 사용 하 여 서비스 검색이 처리 됩니다입니다. 다른 사용자 지정 구현을 포함 됩니다는 그런 다음 **IViewPageActivator** 인터페이스 보기 만들기를 해결할 수 있습니다.

> [!NOTE]
> ASP.NET MVC 3 이후 종속성 주입을 위한 구현 서비스 등록에 대 한 인터페이스를 간소화 했습니다. **되며 IDependencyResolver** 및 **IViewPageActivator** 종속성 주입을 위한 ASP.NET MVC 3 기능의 일부인 합니다.
> 
> **-되며 IDependencyResolver** 인터페이스 이전 IMvcServiceLocator를 대체 합니다. 되며 IDependencyResolver의 구현자는 서비스나 서비스 컬렉션의 인스턴스를 반환 해야 합니다.
>
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> **-IViewPageActivator** 인터페이스는 종속성 주입을 통해 페이지 보기를 인스턴스화하기 하는 방법을 보다 세부적으로 제어를 제공 합니다. 구현 하는 클래스 **IViewPageActivator** 인터페이스는 인스턴스 컨텍스트 정보를 사용 하 여 보기를 만들 수 있습니다.
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]


1. 만들기는 /**팩터리** 프로젝트의 루트 폴더에는 폴더입니다.
2. 포함 **CustomViewPageActivator.cs** 에서 솔루션에 **원본/자산 / /** 를 **팩터리** 폴더입니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 **/Factories** 폴더를 **추가 | 기존 항목** 선택한 후 **CustomViewPageActivator.cs**합니다. 이 클래스가 구현 하는 **IViewPageActivator** Unity 컨테이너를 보유 하는 인터페이스입니다.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > **CustomViewPageActivator** Unity 컨테이너를 사용 하 여 뷰 만들기를 관리 합니다.
3. 포함 **UnityDependencyResolver.cs** 에서 파일을 **/소스/자산** 를 **/Factories** 폴더입니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 **/Factories** 폴더를 **추가 | 기존 항목** 선택한 후 **UnityDependencyResolver.cs** 파일입니다.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > **UnityDependencyResolver** 클래스는 Unity에 대 한 사용자 지정 DependencyResolver 합니다. Unity 컨테이너 내 서비스를 찾을 수 없는 경우 기본 해결 프로그램 invocated 됩니다.

다음 태스크에서 모델 뷰와 서비스의 위치를 알 수 있도록 두 구현 모두 등록 됩니다.

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a>작업 3-Unity 컨테이너 내에서 종속성 주입을 등록 합니다.

이 작업을 함께 작동 하는 종속성 주입을 확인 하는 모든 이전 것을 추가 합니다.

지금까지 솔루션에 다음과 같은 요소가 있습니다.

- A **찾아보기** 에서 상속 되는 보기 **MyBaseClass** 소비 및 **MessageService**합니다.
- 중간 클래스-**MyBaseClass**-이 서비스 인터페이스에 대 한 선언 하는 종속성 주입 합니다.
- 서비스-A **MessageService** -및 해당 인터페이스 **IMessageService**합니다.
- -Unity에 대 한 사용자 지정 종속성 확인자 **UnityDependencyResolver** -서비스 검색을 다루는입니다.
- 뷰 페이지 활성기- **CustomViewPageActivator** -하는 페이지를 만듭니다.

삽입할 **찾아보기** 보기는 이제 등록 사용자 지정 종속성 확인자 Unity 컨테이너에 있습니다.

1. 열기 **Bootstrapper.cs** 파일입니다.
2. 인스턴스 등록 **MessageService** Unity 컨테이너 서비스를 초기화할 수에:

    (코드 조각- *ASP.NET 종속성 주입-Ex02-랩 레지스터 메시지 서비스*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. 에 대 한 참조를 추가 **MvcMusicStore.Factories** 네임 스페이스입니다.

    (코드 조각- *ASP.NET 종속성 주입-Ex02-랩 팩터리 Namespace*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. 등록 **CustomViewPageActivator** Unity 컨테이너로 뷰 페이지 활성기를로:

    (코드 조각- *ASP.NET 종속성 주입-Ex02-랩 레지스터 CustomViewPageActivator*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. ASP.NET MVC 4 기본 종속성 확인자의 인스턴스로 대체 **UnityDependencyResolver**합니다. 이 작업을 수행 하려면 대체 **Initialise** 메서드를 다음 코드로 콘텐츠:

    (코드 조각- *ASP.NET 종속성 주입-Ex02-랩 업데이트 종속성 확인자*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > ASP.NET MVC는 기본 종속성 확인자 클래스를 제공합니다. Unity에 작성 한 것으로 사용자 지정 종속성 확인자를 사용 하려면이 확인자 교체에 있습니다.

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>작업 4-응용 프로그램 실행

이 작업에서는 저장소 브라우저 서비스를 사용 하 고 이미지와 검색 한 메시지를 표시 합니다. 응용 프로그램을 실행 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행합니다.
2. 클릭 **록** 참조 고 장르 메뉴 내에서 방법을 **MessageService** 뷰에 삽입 된 고 환영 메시지와 이미지를 로드 합니다. 이 예제에 진입 하 고 &quot; **록**&quot;:

    ![MVC Music Store 보기 주입](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC Music Store 보기 삽입")

    *MVC Music Store 보기 삽입*
3. 브라우저를 닫습니다.

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a>연습 3: 작업 필터를 삽입합니다.

이전 실습 랩에서 **사용자 지정 작업 필터** 사용자 지정 필터 및 삽입 작업을 수행한 합니다. 이 연습에서는 Unity 컨테이너를 사용 하 여 종속성 주입으로 필터를 삽입 하는 방법에 설명 합니다. 이렇게 하려면 추가 합니다 Music Store 솔루션에 사용자 지정 작업 필터를 사이트의 활동을 추적 합니다.

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a>1-추적 필터를 포함 하 여 솔루션의 작업

이 작업에 포함할 음악 스토어 추적 이벤트에 사용자 지정 작업 필터. 사용자 지정 작업 필터도 개념 이미에서 처리 되는 이전 랩 &quot;사용자 지정 작업 필터&quot;,에서는 바로이 랩의 자산 폴더에서 필터 클래스를 포함 하 고 다음 Unity에 대 한 필터 공급자를 만듭니다.

1. 열기는 **시작** 솔루션에 있는 **Source\Ex03-삽입 작업 Filter\Begin** 폴더입니다. 그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.

    1. 제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면. 이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.
    2. 에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.
    3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.

    > [!NOTE]
    > NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다. NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
    > 
    > 자세한 내용은이 문서를 참조 하십시오.: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)합니다.
2. 포함 **TraceActionFilter.cs** 에서 파일을 **/소스/자산** 를 **필터링/** 폴더입니다.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > 이 사용자 지정 작업 필터는 ASP.NET 추적을 수행합니다. 확인할 수 있습니다 &quot;로컬 ASP.NET MVC 4 및 작업 필터를 동적&quot; 추가 참조에 대 한 랩입니다.
3. 빈 클래스 추가 **FilterProvider.cs** 프로젝트 폴더에   **/필터링 합니다.**
4. 추가 **System.Web.Mvc** 및 **Microsoft.Practices.Unity** 네임 스페이스에 **FilterProvider.cs**합니다.

    (코드 조각- *ASP.NET 종속성 주입-Ex03-랩 필터 공급자 네임 스페이스 추가*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. 클래스에서 상속 **IFilterProvider** 인터페이스입니다.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. 추가 **IUnityContainer** 속성에는 **FilterProvider** 클래스, 한 다음 컨테이너를 할당 하는 클래스 생성자를 만듭니다.

    (코드 조각- *ASP.NET 종속성 주입-Ex03-랩 필터 공급자 생성자*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > 필터 공급자 클래스 생성자를 만들지는 **새** 내부의 개체입니다. 컨테이너를 매개 변수로 전달 하 고 Unity 종속성 해결 됩니다.
7. 에 **FilterProvider** 클래스, 메서드를 구현 **GetFilters** 에서 **IFilterProvider** 인터페이스입니다.

    (코드 조각- *ASP.NET 종속성 주입-Ex03-랩 필터 공급자 GetFilters*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a>작업 2-등록 및 필터 사용

이 태스크에서는 사이트 관리를 설정 합니다. 이렇게 하려면 필터를 등록 합니다 **Bootstrapper.cs BuildUnityContainer** 메서드 추적을 시작 합니다.

1. 열기 **Web.config** System.Web 그룹에서 사용 추적 추적 및 프로젝트 루트에 있는 합니다.

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. 열기 **Bootstrapper.cs** 프로젝트 루트에 있습니다.
3. 에 대 한 참조 추가 **MvcMusicStore.Filters** 네임 스페이스입니다.

    (코드 조각- *ASP.NET 종속성 주입-Ex03-랩 부트스트래퍼 네임 스페이스 추가*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. 선택 된 **BuildUnityContainer** 메서드와 Unity 컨테이너에 있는 필터를 등록 합니다. 작업 필터와 필터 공급자를 등록 해야 합니다.

    (코드 조각- *ASP.NET 종속성 주입-Ex03-랩 레지스터 FilterProvider 및 ActionFilter*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>작업 3-응용 프로그램 실행

이 태스크에서는 응용 프로그램을 실행 하 고 사용자 지정 작업 필터는 활동을 추적는 테스트 됩니다.

1. **F5** 키를 눌러 응용 프로그램을 실행합니다.
2. 클릭 **록** 장르 메뉴 내에서. 하려면 더 많은 장르를 찾아볼 수 있습니다.

    ![Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "음악 스토어")

    *Music Store*
3. 찾아 **/Trace.axd** 을 클릭 한 다음 응용 프로그램 추적을 보려면 **세부 정보 보기**합니다.

    ![응용 프로그램 추적 로그](aspnet-mvc-4-dependency-injection/_static/image12.png "응용 프로그램 추적 로그")

    *응용 프로그램 추적 로그*

    ![응용 프로그램 추적-요청 정보](aspnet-mvc-4-dependency-injection/_static/image13.png "응용 프로그램 추적-요청 정보")

    *응용 프로그램 추적-요청 세부 정보*
4. 브라우저를 닫습니다.

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 랩을 완료 하 여 NuGet 패키지를 사용 하 여 Unity를 통합 하 여 ASP.NET MVC 4의 종속성 주입을 사용 하는 방법을 배웠습니다. 이 위해 컨트롤러, 뷰 및 작업 필터 내부 종속성 주입을 사용 했습니다.

다음과 같은 개념 포함 되지 않았습니다.

- ASP.NET MVC 4 종속성 주입 기능
- Unity 통합 Unity.Mvc3 NuGet 패키지를 사용 하 여
- 컨트롤러의 종속성 주입
- 보기의 종속성 주입
- 작업 필터의 종속성 주입

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 a: 설치 Visual Studio Express 2012 for Web

설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 버전을 사용 하 여  **[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** . 다음 지침을 설치 하는 데 필요한 단계를 안내 하 *Visual studio Express 2012 for Web* 를 사용 하 여 *Microsoft 웹 플랫폼 설치 관리자*합니다.

1. 로 이동 [ [https://go.microsoft.com/? linkid = 9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)합니다. 또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; *Visual Studio Express 2012 for Web Windows Azure SDK와*&quot;합니다.
2. 클릭 **지금 설치**합니다. 없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.
3. 한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.

    ![Visual Studio Express 설치](aspnet-mvc-4-dependency-injection/_static/image14.png "Visual Studio Express 설치")

    *Visual Studio Express 설치*
4. 모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.

    ![사용 조건 동의](aspnet-mvc-4-dependency-injection/_static/image15.png)

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](aspnet-mvc-4-dependency-injection/_static/image16.png)

    *설치 진행률*
6. 설치가 완료 되 면 클릭 **마침**합니다.

    ![설치 완료](aspnet-mvc-4-dependency-injection/_static/image17.png)

    *설치 완료*
7. 클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.
8. Visual Studio Express for Web을 열려면로 이동는 **시작** 화면를 쓰기 시작할 &quot; **VS Express**&quot;, 클릭는 **VS Express for Web** 바둑판식 배열입니다.

    ![웹 타일에 대 한 VS Express](aspnet-mvc-4-dependency-injection/_static/image18.png)

    *웹 타일에 대 한 VS Express*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>부록 b: 코드 조각을 사용 하 여

코드 조각 바로 쉽게 얻습니다 필요한 코드를 수 있습니다. 랩 문서는 알려 정확 하 게 사용 가능 시기, 다음 그림에 나와 있는 것 처럼 합니다.

![Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여](aspnet-mvc-4-dependency-injection/_static/image19.png "Visual Studio를 사용 하 여 코드 조각을 프로젝트에 코드를 삽입 하려면")

*Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여*

***키보드 (C#만)를 사용 하 여 코드 조각을 추가 하려면***

1. 코드를 삽입 하려는 위치에 커서를 놓습니다.
2. 공백 또는 하이픈만) (없이 코드 조각 이름을 입력 하기 시작 합니다.
3. IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.
4. 올바른 코드 조각 선택 (또는 전체 코드 조각이 이름이 선택 될 때까지 입력 유지).
5. 커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.

![코드 조각 이름을 입력 하기 시작](aspnet-mvc-4-dependency-injection/_static/image20.png "조각 이름을 입력 하기 시작")

*코드 조각 이름을 입력 하기 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각 선택](aspnet-mvc-4-dependency-injection/_static/image21.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")

*Tab 키를 눌러 강조 표시 된 코드 조각 선택*

![확장 하 고 Tab 키를 눌러 다시 코드 조각](aspnet-mvc-4-dependency-injection/_static/image22.png "확장 하 고 Tab 키를 눌러 다시 코드 조각")

*확장 하 고 Tab 키를 눌러 다시 코드 조각*

***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1입니다. 코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.

1. 선택 **조각 삽입** 이어서 **내 코드 조각**합니다.
2. 클릭 하 여 목록에서 관련 조각을 선택 합니다.

![코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-dependency-injection/_static/image23.png "코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추 클릭")

*코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭*

![클릭 하 여 목록에서 관련 조각을 선택](aspnet-mvc-4-dependency-injection/_static/image24.png "클릭 하 여 목록에서 관련 조각을 선택")

*클릭 하 여 목록에서 관련 조각을 선택합니다*
