---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: ASP.NET MVC 4 종속성 주입 | Microsoft Docs
author: rick-anderson
description: 참고:이 실습 랩에서 ASP.NET MVC 및 ASP.NET MVC 4 필터에 대 한 기본 지식이 있다고 가정 합니다. ASP.NET MVC 4 필터 하기 전에 사용 하지 않은 rec... 하는 경우
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 715444a6fbf491d7b99918294cfd2d0d0216cd09
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388046"
---
# <a name="aspnet-mvc-4-dependency-injection"></a>ASP.NET MVC 4 종속성 주입

[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 학습 키트 다운로드](https://aka.ms/webcamps-training-kit)

이 실습 랩 기본 지식이 있다고 가정 **ASP.NET MVC** 하 고 **필터링 하는 ASP.NET MVC 4**합니다. 사용 하지 않은 경우 **ASP.NET MVC 4 필터링** 이전 좋습니다 이동해 **ASP.NET MVC 사용자 지정 작업 필터** 실습 랩입니다.

> [!NOTE]
> 웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 된 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다. 이 랩에 특정 프로젝트에서 제공 됩니다 [ASP.NET MVC 4 종속성 주입](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection)합니다.

**객체 지향 프로그래밍** 패러다임 개체가 함께 동작 공동 작업 모델 참가자와 소비자가 있는 합니다. 물론이 통신 모델 개체 및 복잡성이 증가 하는 경우 관리 하기가 점점 구성 요소 간의 종속성을 생성 합니다.

![종속성을 클래스 및 모델 복잡성](aspnet-mvc-4-dependency-injection/_static/image1.png "종속성 클래스 및 복잡성을 모델")

*클래스 종속성 및 모델의 복잡성*

에 대 한 번쯤은 들어봤을 겁니다 합니다 **팩터리 패턴** 및 인터페이스와 서비스를 사용 하 여 클라이언트 개체 서비스 위치에 대 한 책임 많습니다 구현 간의 분리 합니다.

종속성 주입 패턴은 Inversion of Control의 특정 구현 합니다. **반전 (IoC) 제어** 개체 들은 작업할 때 서로 다른 개체를 만들지 마십시오 의미 합니다. 대신 외부 소스 (예를 들어, xml 구성 파일)에서 필요한 개체를 얻을 수 있습니다.

**DI (종속성 주입)** 은 있음을 나타내고이 수행한 개체 개입 없이 일반적으로 생성자 매개 변수를 전달 하는 프레임 워크 구성 요소 속성을 설정 합니다.

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a>종속성 주입 (DI) 디자인 패턴

높은 수준에서 종속성 주입의 목표는 클라이언트 클래스 (예: *는 골퍼*) 인터페이스를 충족 하는 것을 요구 (예: *IClub*). 구체적인 형식 이란를 고려 하지 않습니다 (예: *WoodClub, IronClub, WedgeClub* 또는 *PutterClub*), 문제를 해결 하려면 다른 사용자가 (좋은 예를 들어 *caddy*). ASP.NET MVC의 종속성 확인자를 사용 하면 어딘가 다른 종속성 논리를 등록할 수 있습니다 (예: 컨테이너 또는 *클럽 모음*).

![종속성 주입 다이어그램](aspnet-mvc-4-dependency-injection/_static/image2.png "종속성 주입 그림")

*종속성 주입-골프 비유*

종속성 주입 패턴 및 Inversion of Control을 사용 하는 이점은 다음과 같습니다.

- 클래스 결합을 줄일 수
- 코드 재사용 증가
- 코드 유지 가능성 향상
- 응용 프로그램 테스트 개선

> [!NOTE]
> 종속성 주입 추상 팩터리 디자인 패턴을 따라 비교 되어 있지만 두 방법 간에 약간의 차이가 있습니다. DI는 프레임 워크는 팩터리 및 등록된 된 서비스를 호출 하 여 종속성을 해결 하기 위해 작업 뒤에 있습니다.


종속성 주입 패턴을 이해 했으므로 배웁니다이 랩 전체 ASP.NET MVC 4에서 적용 하는 방법. 종속성 주입을 사용 하 여 시작 합니다 **컨트롤러** 데이터베이스 액세스 서비스를 포함 하도록 합니다. 다음으로, 종속성 주입에 적용할 합니다 **뷰** 서비스를 사용 하 여 정보를 표시 합니다. 마지막으로 확장 하면는 DI를 ASP.NET MVC 4 필터에 솔루션의 사용자 지정 작업 필터를 삽입 합니다.

이 실습 랩에서 학습할 방법:

- Unity를 사용 하 여 NuGet 패키지를 사용 하 여 종속성 주입을 위한 ASP.NET MVC 4를 통합
- ASP.NET MVC 컨트롤러 내에서 사용 하 여 종속성 주입
- ASP.NET MVC 뷰 내에서 사용 하 여 종속성 주입
- 내 ASP.NET MVC 작업 필터를 사용 하 여 종속성 주입

> [!NOTE]
> 이 랩에서 Unity.Mvc3 NuGet 패키지를 사용 하 여 종속성 확인에 있지만 ASP.NET MVC 4를 사용 하는 종속성 주입 프레임 워크를 조정할 수 있습니다.


<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>전제 조건

이 랩을 완료 하려면 다음 항목이 있어야 합니다.

- [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽을 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>설정

**설치 코드 조각**

편의 위해이 랩에서 함께 관리 하려는 코드의 대부분 제품은 Visual Studio 코드 조각입니다. 설치를 실행 하는 코드 조각 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.

이 문서의 부록 참조할 수 있습니다 사용 하는 방법을 알아보려면 원하는 고 Visual Studio 코드 조각을 사용 하 여 잘 모르는 경우 &quot; [부록 b:를 사용 하 여 코드 조각](#AppendixB)&quot;합니다.

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>연습

이 실습 랩에서 다음 연습으로 구성 됩니다.

1. [연습 1: 컨트롤러 삽입](#Exercise1)
2. [연습 2: 보기 삽입](#Exercise2)
3. [필터를 삽입 하는 연습 3:](#Exercise3)

> [!NOTE]
> 각 실습 동반 되는 **최종** 연습을 완료 한 후 가져와야 결과 솔루션이 포함 된 폴더입니다. 이 연습을 진행 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.


이 랩을 완료 하기 위한 예상 시간: **30 분**합니다.

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a>연습 1: 컨트롤러 삽입

이 연습에서는 Unity는 NuGet 패키지를 사용 하 여 통합 하 여 ASP.NET MVC 컨트롤러에서 종속성 주입을 사용 하는 방법을 배웁니다. 이런 이유로 서비스에서 데이터 액세스 논리를 분리 하기 위해 MvcMusicStore 컨트롤러에 포함 됩니다. 서비스를 활용 하 여 종속성 주입을 사용 하 여 확인 될 컨트롤러 생성자에서 새 종속성을 만듭니다 **Unity**합니다.

이 방법은 덜 결합 된 응용 프로그램을 보다 유연 하 고 유지 관리 하 고 테스트 하는 작업을 쉽게 생성 하는 방법을 표시 됩니다. Unity를 사용한 ASP.NET MVC를 통합 하는 방법 또한 배웁니다.

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a>StoreManager 서비스에 대 한

이제 시작 솔루션에서 제공 하는 MVC Music Store 라는 저장소 컨트롤러 데이터를 관리 하는 서비스를 포함 **StoreService**합니다. 아래 저장소 서비스 구현을 찾을 수 있습니다. 모든 메서드는 모델 엔터티를 반환 하는 참고 합니다.

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

**StoreController** 시작에서 솔루션 이제 소비 **StoreService**합니다. 모든 데이터 참조에서 제거 되었습니다 **StoreController**, 및를 사용 하는 모든 메서드를 변경 하지 않고 현재 데이터 액세스 공급자를 수정 하는 현재 사용 가능한 **StoreService**합니다.

아래에 찾을 수 있습니다 합니다 **StoreController** 구현에 사용 하 여 종속성 **StoreService** 클래스 생성자 내에서.

> [!NOTE]
> 이 연습에 도입 된 종속성 관련이 **Inversion of Control** (IoC).
> 
> 합니다 **StoreController** 클래스 생성자를 받습니다는 **IStoreService** 클래스 내에서 서비스를 호출 하는 데 필수적인 형식 매개 변수입니다. 그러나 **StoreController** 를 기본 (매개 변수가 없는 생성자) 모든 컨트롤러는 ASP.NET MVC를 사용 하 여 작업을 포함 해야 하는 구현 하지 않습니다.
> 
> 종속성을 해결 하려면 컨트롤러 (지정 된 형식의 모든 개체를 반환 하는 클래스)는 추상 팩터리에서 만든 수 해야 합니다.


[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> 클래스에서 선언 된 매개 변수가 없는 생성자는 서비스 개체를 전송 하지 않고는 StoreController 만들 하려고 할 때 오류를 받습니다.


<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a>작업 1-응용 프로그램 실행

이 태스크에서는 데이터 액세스 응용 프로그램 논리와 분리 하는 저장소 컨트롤러에 서비스를 포함 하는 시작 응용 프로그램을 실행 합니다.

응용 프로그램을 실행할 때 컨트롤러 서비스를 기본적으로 매개 변수로 전달 하지는 예외를 받습니다.

1. 엽니다는 **시작** 솔루션에 있는 **Controller\Begin Source\Ex01 삽입**합니다.

   1. 일부 누락 된 NuGet 패키지를 다운로드 해야 하기 전에 계속 합니다. 이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다. NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
2. 키를 눌러 **ctrl+f5** 디버깅 하지 않고 응용 프로그램을 실행 합니다. 오류 메시지가 표시 됩니다 &quot; **이 개체에 대해 정의 된 매개 변수가 없는 생성자가 없습니다**&quot;:

    ![ASP.NET MVC 시작 응용 프로그램을 실행 하는 동안 오류가 발생 했습니다](aspnet-mvc-4-dependency-injection/_static/image3.png "ASP.NET MVC 시작 응용 프로그램을 실행 하는 동안 오류가 발생 했습니다")

    *ASP.NET MVC 시작 응용 프로그램을 실행 하는 동안 오류가 발생 했습니다*
3. 브라우저를 닫습니다.

다음 단계를이 컨트롤러에 필요한 종속성을 주입할 음악 스토어 솔루션에서 작동 합니다.

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a>작업 2-MvcMusicStore 솔루션에 포함 하 여 Unity

이 작업에서는 포함 됩니다 **Unity.Mvc3** 솔루션에 NuGet 패키지.

> [!NOTE]
> Unity.Mvc3 패키지 ASP.NET MVC 3에 대 한 디자인 되었지만 ASP.NET MVC 4를 사용 하 여 완전히 호환 됩니다.
> 
> Unity 지원 (옵션)를 사용 하 여 간단 하 고 확장 가능한 종속성 주입 컨테이너를 예를 들어 이며 인터 셉 션을 입력 합니다. 모든 유형의.NET 응용 프로그램에서 사용 하기 위해 범용 컨테이너입니다. 포함 하 여 종속성 주입 메커니즘에 있는 모든 일반적인 기능을 제공 합니다: 개체 만들기, 컨테이너에 구성 요소 구성 지연 하 여 런타임 및 유연성에 대 한 종속성을 지정 하 여 요구 사항의 추상화 합니다.


1. 설치할 **Unity.Mvc3** NuGet 패키지에는 **MvcMusicStore** 프로젝트입니다. 이 작업을 수행 하려면 엽니다는 **패키지 관리자 콘솔** 에서 **뷰** | **기타 Windows**합니다.
2. 다음 명령을 실행합니다.

    PMC

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    ![Unity.Mvc3 NuGet 패키지를 설치](aspnet-mvc-4-dependency-injection/_static/image4.png "Unity.Mvc3 NuGet 패키지를 설치 합니다.")

    *Unity.Mvc3 NuGet 패키지를 설치합니다.*
3. 한 번 합니다 **Unity.Mvc3** 패키지를 설치, 파일 및 Unity 구성을 단순화 하기 위해 자동으로 추가 하는 폴더를 탐색 합니다.

    ![Unity.Mvc3 패키지 설치](aspnet-mvc-4-dependency-injection/_static/image5.png "Unity.Mvc3 패키지 설치")

    *Unity.Mvc3 패키지 설치*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-applicationstart"></a>작업 3-Global.asax.cs 응용 프로그램에서 등록 Unity\_시작

이 태스크에서는 업데이트를 **응용 프로그램\_시작** 에 있는 메서드 **Global.asax.cs** Unity 부트스트래퍼 이니셜라이저를 호출 하 고 그런 다음 등록 하는 부트스트래퍼 파일을 업데이트 하려면 서비스 및 종속성 주입을 위해 사용 하 여 컨트롤러입니다.

1. 이제 Unity 컨테이너를 초기화 하는 파일인 부트스트래퍼 및 종속성 확인자를 연결 합니다. 이 작업을 수행 하려면 엽니다 **Global.asax.cs** 내에서 다음 강조 표시 된 코드를 추가 합니다 **응용 프로그램\_시작** 메서드.

    (코드 조각- *ASP.NET 종속성 주입 랩-Ex01-Unity 초기화*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. 오픈 **Bootstrapper.cs** 파일입니다.
3. 네임 스페이스를 포함 합니다. **MvcMusicStore.Services** 하 고 **MusicStore.Controllers**합니다.

    (코드 조각- *네임 스페이스를 추가 하는 ASP.NET 종속성 주입-Ex01-랩 부트스트래퍼*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. 바꿉니다 **BuildUnityContainer** 메서드의 저장소 컨트롤러 및 저장소 서비스를 등록 하는 다음 코드를 사용 하 여 콘텐츠입니다.

    (코드 조각- *ASP.NET 종속성 주입-Ex01-랩 등록 저장소 컨트롤러 및 서비스*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>작업 4-응용 프로그램 실행

이 태스크는 이제 로드할 수 있습니다 Unity를 포함 한 후 확인 하려면 응용 프로그램을 실행 합니다.

1. 키를 눌러 **F5** 응용 프로그램을 실행 하려면 응용 프로그램 오류 메시지를 표시 하지 않고 로드 이제 해야 합니다.

    ![종속성 주입을 사용 하 여 응용 프로그램을 실행](aspnet-mvc-4-dependency-injection/_static/image6.png "종속성 주입을 사용 하 여 응용 프로그램을 실행 합니다.")

    *종속성 주입을 사용 하 여 응용 프로그램을 실행합니다.*
2. 이동할 **스토어**합니다. 이렇게 하면 **StoreController**를 사용 하 여 이제 만들어지는 **Unity**합니다.

    ![MVC Music Store](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC Music Store")

    *MVC Music Store*
3. 브라우저를 닫습니다.

다음 연습에서 ASP.NET MVC 뷰 및 작업 필터 내에서 사용 하는 종속성 주입 범위를 확장 하는 방법을 배웁니다.

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a>연습 2: 보기 삽입

이 연습에서는 Unity 통합에 대 한 ASP.NET MVC 4의 새로운 기능을 사용 하 여 보기에 종속성 주입을 사용 하는 방법을 배웁니다. 이 작업을 수행 하기 위해 메시지 및 아래 이미지로 표시 되는 저장소 찾아보기 보기 내에서 사용자 지정 서비스를 호출 합니다.

그런 다음 Unity를 사용 하 여 프로젝트를 통합 하 고 종속성을 삽입 하는 사용자 지정 종속성 확인자를 만듭니다 됩니다.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a>작업 1-서비스를 사용 하는 뷰 만들기

이 태스크에서는 새 종속성을 생성 하는 서비스 호출을 수행 하는 뷰를 만듭니다. 이 솔루션에 포함 된 간단한 메시징 서비스에서 서비스 구성 됩니다.

1. 엽니다는 **시작** 솔루션에는 **View\Begin Source\Ex02 삽입** 폴더. 그렇지 않은 경우 계속 사용할 수도 있습니다는 **최종** 이전 연습을 완료 하 여 가져온 솔루션입니다.

   1. 제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다. 이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다. NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
      > 
      > 자세한 내용은이 문서를 참조 하세요. [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)합니다.
2. 포함 합니다 **MessageService.cs** 및 **IMessageService.cs** 클래스에는 **\Assets 원본** 폴더에 **/서비스**합니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 **Services** 선택한 폴더 **기존 항목 추가**합니다. 파일의 위치를 찾아 포함 합니다.

    ![메시지 서비스 및 서비스 인터페이스를 추가](aspnet-mvc-4-dependency-injection/_static/image8.png "메시지 서비스 및 서비스 인터페이스를 추가 합니다.")

    *추가 메시지 서비스 및 서비스 인터페이스*

    > [!NOTE]
    > **IMessageService** 인터페이스에 의해 구현 되는 두 속성을 정의 합니다 **MessageService** 클래스입니다. 이러한 속성-**메시지** 하 고 **ImageUrl**-표시할 메시지 및 이미지의 URL을 저장 합니다.
3. 폴더를 만듭니다 **/pages** 프로젝트의 루트 폴더를 추가한 다음 기존 클래스 **MyBasePage.cs** 에서 **Source\Assets**합니다. 상속 하는 기본 페이지는 다음 구조를 가집니다.

    ![페이지 폴더](aspnet-mvc-4-dependency-injection/_static/image9.png "페이지 폴더")

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. 오픈 **Browse.cshtml** 에서 확인할 **/뷰/저장** 폴더에서 상속 하 고 **MyBasePage.cs**합니다.

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. 에 **찾아보기** 보기에서 호출을 추가 **MessageService** 이미지 및 서비스에서 검색 메시지를 표시 합니다.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a>작업 2-사용자 지정 종속성 확인자 및 사용자 지정 뷰 페이지 활성기를 포함 하 여

이전 작업에서 내부 서비스 호출을 수행 하려면 뷰 내에서 새 종속성을 주입 합니다. ASP.NET MVC 종속성 주입 인터페이스를 구현 하 여 해당 종속성을 확인 되는 이제 **IViewPageActivator** 하 고 **IDependencyResolver**합니다. 구현 솔루션에 포함 됩니다 **IDependencyResolver** 는 Unity를 사용 하 여 서비스 검색을 사용 하 여 처리 됩니다. 다른 사용자 지정 구현이 포함 됩니다 차례로 **IViewPageActivator** 뷰의 생성을 해결할 수 있는 인터페이스입니다.

> [!NOTE]
> ASP.NET MVC 3부터 종속성 주입에 대 한 구현을 서비스 등록에 대 한 인터페이스를 간소화 했습니다. **IDependencyResolver** 하 고 **IViewPageActivator** 종속성 주입을 위한 ASP.NET MVC 3 기능의 일부인 합니다.
> 
> **-IDependencyResolver** 인터페이스 이전 IMvcServiceLocator를 대체 합니다. IDependencyResolver의 구현자는 서비스나 서비스 컬렉션의 인스턴스를 반환 해야 합니다.
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> **-IViewPageActivator** 인터페이스는 종속성 주입을 통해 페이지 보기가 인스턴스화될 방법을 보다 세부적으로 제어를 제공 합니다. 구현 하는 클래스 **IViewPageActivator** 인터페이스 컨텍스트 정보를 사용 하 여 인스턴스 보기를 만들 수 있습니다.
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]


1. 만들기는 /**팩터리** 프로젝트의 루트 폴더의 폴더입니다.
2. 포함 **CustomViewPageActivator.cs** 에서 솔루션 **/자산/원본/** 하 **팩터리** 폴더입니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **/Factories** 폴더 **추가 | 기존 항목** 선택한 후 **CustomViewPageActivator.cs**합니다. 이 클래스에서 구현 된 **IViewPageActivator** Unity 컨테이너를 보유 하는 인터페이스입니다.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > **CustomViewPageActivator** Unity 컨테이너를 사용 하 여 뷰를 만드는 관리 담당 합니다.
3. 포함 **UnityDependencyResolver.cs** 에서 파일 **/원본/자산** 하 **/Factories** 폴더입니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **/Factories** 폴더 **추가 | 기존 항목** 선택한 후 **UnityDependencyResolver.cs** 파일입니다.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > **UnityDependencyResolver** 클래스는 Unity에 대 한 사용자 지정 DependencyResolver 합니다. Unity 컨테이너 내에서 서비스를 찾을 수 없는 경우 기본 확인자 invocated 됩니다.

다음 태스크에서 두 구현 모두 모델 뷰와 서비스의 위치를 알 수 있도록 등록 됩니다.

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a>작업 3-Unity 컨테이너 내에서 종속성 주입에 등록

이 태스크에서는 작동 하는 종속성 주입 하기 위해 모든 이전 항목을 추가 합니다.

지금까지 솔루션에는 다음과 같은 요소가 있습니다.

- A **찾아보기** 에서 상속 되는 뷰 **MyBaseClass** 들고 **MessageService**합니다.
- 중간 클래스-**MyBaseClass**-서비스 인터페이스에 대해 선언 된 종속성 주입 된 합니다.
- 서비스-A **MessageService** -및 해당 인터페이스 **IMessageService**합니다.
- Unity-에 대 한 사용자 지정 종속성 확인자 **UnityDependencyResolver** -서비스 검색을 사용 하 여 처리 하는 합니다.
- 뷰 페이지 활성기를- **CustomViewPageActivator** -는 페이지를 만듭니다.

삽입할 **찾아보기** 보기에서는 이제 사용자 지정 종속성 확인자에서에서 등록 Unity 컨테이너입니다.

1. 오픈 **Bootstrapper.cs** 파일입니다.
2. 인스턴스를 등록할 **MessageService** Unity 컨테이너 서비스를 초기화할 수에 합니다.

    (코드 조각- *ASP.NET 종속성 주입-Ex02-랩 등록 메시지 서비스*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. 에 대 한 참조를 추가 **MvcMusicStore.Factories** 네임 스페이스입니다.

    (코드 조각- *ASP.NET 종속성 주입-Ex02-랩 팩터리 Namespace*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. 등록할 **CustomViewPageActivator** Unity 컨테이너에 뷰 페이지 활성기를으로:

    (코드 조각- *ASP.NET 종속성 주입-Ex02-랩 등록 CustomViewPageActivator*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. ASP.NET MVC 4 기본 종속성 확인자 인스턴스의 바꿉니다 **UnityDependencyResolver**합니다. 이 작업을 수행 하려면 바꿉니다 **Initialise** 콘텐츠를 다음 코드로 메서드:

    (코드 조각- *ASP.NET 종속성 주입-Ex02-랩 업데이트 종속성 확인자*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > ASP.NET MVC 기본 종속성 확인자 클래스를 제공 합니다. 사용자 지정 종속성 확인 자의 unity에 작성 한 것을 사용 하려면이 확인자를 교체 해야 합니다.

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>작업 4-응용 프로그램 실행

이 태스크에서는 저장소 브라우저 서비스를 사용 하 고 이미지 및 검색 메시지를 표시 하는지 확인 하려면 응용 프로그램을 실행 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행합니다.
2. 클릭 **Rock** 장르 메뉴 및 참조 내에서 하는 방법을 **MessageService** 뷰에 삽입 된 및 환영 메시지 및 이미지를 로드 합니다. 에 진입 하 고이 예에서 &quot; **Rock**&quot;:

    ![MVC Music Store-보기 주입](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC Music Store-보기 주입")

    *MVC Music Store-보기 주입*
3. 브라우저를 닫습니다.

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a>연습 3: 삽입 작업 필터

이전 실습 랩에서 **사용자 지정 작업 필터** 필터 사용자 지정 및 삽입 작업을 수행한 합니다. 이 연습에서는 Unity 컨테이너를 사용 하 여 종속성 주입을 사용 하 여 필터를 주입 하는 방법을 배웁니다. 이렇게 하려면 추가 Music Store 솔루션에는 사이트의 작업을 추적 하는 사용자 지정 작업 필터.

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a>작업 1-추적 필터를 포함 하 여 솔루션의

이 태스크에서는 Music Store에서 사용자 지정 작업 필터 추적 이벤트를 포함할가 있습니다. 사용자 지정 작업 필터로 개념 이미 처리할지 이전 랩에서 &quot;사용자 지정 작업 필터&quot;,에서는 바로이 랩의 자산 폴더에서 필터 클래스를 포함 하 고 다음 Unity에 대 한 필터 공급자를 만듭니다.

1. 엽니다는 **시작** 솔루션에는 **Source\Ex03-삽입 작업 Filter\Begin** 폴더. 그렇지 않은 경우 계속 사용할 수도 있습니다는 **최종** 이전 연습을 완료 하 여 가져온 솔루션입니다.

   1. 제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다. 이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.
   2. 에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.
   3. 마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.

      > [!NOTE]
      > NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다. NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다. 이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.
      > 
      > 자세한 내용은이 문서를 참조 하세요. [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)합니다.
2. 포함 **TraceActionFilter.cs** 에서 파일 **/원본/자산** 하 **필터링/** 폴더입니다.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > 이 사용자 지정 작업 필터는 ASP.NET 추적을 수행합니다. 확인할 수 있습니다 &quot;ASP.NET MVC 4 로컬 및 동적 작업 필터&quot; 랩 더 많은 참조 합니다.
3. 빈 클래스를 추가 **FilterProvider.cs** 에서 프로젝트 폴더에   **/필터링 합니다.**
4. 추가 합니다 **System.Web.Mvc** 하 고 **Microsoft.Practices.Unity** 네임 스페이스 **FilterProvider.cs**합니다.

    (코드 조각- *ASP.NET 종속성 주입-Ex03-랩 필터 공급자 네임 스페이스 추가*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. 클래스에서 상속 **IFilterProvider** 인터페이스입니다.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. 추가 **IUnityContainer** 속성에는 **FilterProvider** 클래스를 만든 다음 컨테이너를 할당 하기 위해 클래스 생성자입니다.

    (코드 조각- *ASP.NET 종속성 주입-Ex03-랩 필터 공급자 생성자*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > 필터 공급자 클래스 생성자를 만들지는 **새** 내부 개체입니다. 컨테이너 매개 변수로 전달 하 고 Unity 종속성 해결 됩니다.
7. 에 **FilterProvider** 클래스, 메서드를 구현 **GetFilters** 에서 **IFilterProvider** 인터페이스입니다.

    (코드 조각- *ASP.NET 종속성 주입-Ex03-랩 필터 공급자 GetFilters*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a>작업 2-등록 하 고 필터를 사용 하도록 설정

이 태스크에서는 사이트 추적 사용 하도록 설정 됩니다. 이렇게 하려면 필터를 등록할 **Bootstrapper.cs BuildUnityContainer** 추적을 시작 하는 방법.

1. 오픈 **Web.config** System.Web 그룹에서 사용 추적 추적 고 프로젝트 루트에 있습니다.

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. 오픈 **Bootstrapper.cs** 프로젝트 루트에서.
3. 에 대 한 참조를 추가 합니다 **MvcMusicStore.Filters** 네임 스페이스입니다.

    (코드 조각- *네임 스페이스를 추가 하는 ASP.NET 종속성 주입-Ex03-랩 부트스트래퍼*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. 선택 된 **BuildUnityContainer** 메서드 및 Unity 컨테이너에서 필터를 등록 합니다. 작업 필터와 필터 공급자를 등록 해야 합니다.

    (코드 조각- *ASP.NET 종속성 주입-Ex03-랩 등록 FilterProvider 및 ActionFilter*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>작업 3-응용 프로그램 실행

이 태스크에서는 응용 프로그램을 실행 하 고 사용자 지정 작업 필터는 활동 추적는 테스트 됩니다.

1. **F5** 키를 눌러 응용 프로그램을 실행합니다.
2. 클릭 **Rock** 장르 메뉴 내에서. 하려는 경우 자세한 장르를 찾아볼 수 있습니다.

    ![Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Music Store")

    *Music Store*
3. 이동할 **/Trace.axd** 페이지를 선택한 다음 클릭 응용 프로그램 추적을 보려는 **세부 정보 보기**합니다.

    ![응용 프로그램 추적 로그](aspnet-mvc-4-dependency-injection/_static/image12.png "응용 프로그램 추적 로그")

    *응용 프로그램 추적 로그*

    ![응용 프로그램 추적-요청 세부 정보](aspnet-mvc-4-dependency-injection/_static/image13.png "응용 프로그램 추적-요청 정보")

    *응용 프로그램 추적-요청 세부 정보*
4. 브라우저를 닫습니다.

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습을 완료 하 여 NuGet 패키지를 사용 하는 Unity를 통합 하 여 ASP.NET MVC 4에서 종속성 주입을 사용 하는 방법을 배웠습니다. 이 위해 컨트롤러, 보기 및 작업 필터 내에서 종속성 주입을 사용 했습니다.

다음 개념 적용 되었습니다.

- ASP.NET MVC 4 종속성 주입 기능
- Unity 통합 Unity.Mvc3 NuGet 패키지를 사용 하 여
- 컨트롤러에서 종속성 주입
- 뷰에 종속성 주입
- 작업 필터의 종속성 주입

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 a: 설치 Visual Studio Express 2012 for Web

설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 사용 하 여 버전을 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**. 다음 지침을 설치 하는 데 필요한 단계를 안내 *Visual studio Express 2012 for Web* 사용 하 여 *Microsoft Web Platform Installer*합니다.

1. 로 이동 [ [ https://go.microsoft.com/? linkid 9810169 =](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)합니다. 또는, 이미 설치한 경우 웹 플랫폼 설치 관리자를 열 수 있습니다 하 고 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Windows Azure SDK를 사용 하 여 Web</em>&quot;합니다.
2. 클릭할 **지금 설치**합니다. 없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 리디렉션됩니다.
3. 한 번 **웹 플랫폼 설치 관리자** 열려 있는 경우 클릭 **설치** 는 설치를 시작 합니다.

    ![Visual Studio Express를 설치](aspnet-mvc-4-dependency-injection/_static/image14.png "Visual Studio Express를 설치 합니다.")

    *Visual Studio Express를 설치 합니다.*
4. 모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.

    ![사용 조건에 동의](aspnet-mvc-4-dependency-injection/_static/image15.png)

    *사용 조건에 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](aspnet-mvc-4-dependency-injection/_static/image16.png)

    *설치 진행률*
6. 설치가 완료 되 면 클릭 **완료**합니다.

    ![설치 완료](aspnet-mvc-4-dependency-injection/_static/image17.png)

    *설치 완료*
7. 클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.
8. 로 Visual Studio Express for Web을 열려면 합니다 **시작** 화면 및 쓰기를 시작 &quot; **VS Express**&quot;를 클릭 합니다 **VS Express for Web** 타일입니다.

    ![VS Express for Web 타일](aspnet-mvc-4-dependency-injection/_static/image18.png)

    *VS Express for Web 타일*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>부록 b: 코드 조각 사용

코드 조각을 사용 하 여 결정적인 순간에 필요한 모든 코드를 해야 합니다. 랩 문서가 알려줍니다 정확 하 게 사용할 수 있는 시기를 다음 그림과 같습니다.

![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드를 삽입할](aspnet-mvc-4-dependency-injection/_static/image19.png "프로젝트에 코드를 삽입 하는 Visual Studio를 사용 하 여 코드 조각을")

*프로젝트에 코드를 삽입 하려면 Visual Studio 코드 조각 사용*

***키보드 (C#만 해당)를 사용 하 여 코드 조각을 추가 하려면***

1. 코드를 삽입 하려는 위치에 커서를 놓습니다.
2. 시작 (공백 없이 하이픈) 조각 이름을 입력 합니다.
3. IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.
4. 올바른 코드 조각을 선택 합니다 (또는 전체 코드 조각 이름을 선택 될 때까지 입력 유지).
5. 커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.

![코드 조각 이름을 입력](aspnet-mvc-4-dependency-injection/_static/image20.png "조각 이름을 입력 하기 시작")

*코드 조각 이름을 입력 하기 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각을](aspnet-mvc-4-dependency-injection/_static/image21.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")

*Tab 키를 눌러 강조 표시 된 코드 조각 선택*

![Tab 키를 다시 코드 조각 확장 됩니다](aspnet-mvc-4-dependency-injection/_static/image22.png "다시 Tab 키를 누릅니다 하 고 코드 조각에서는 확장")

*Tab 키를 다시 및 코드 조각에서는 확장*

***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가할*** 1입니다. 코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.

1. 선택 **코드 조각 삽입** 뒤 **내 코드 조각**합니다.
2. 클릭 하 여 목록에서 관련 코드 조각을 선택 합니다.

![코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-dependency-injection/_static/image23.png "코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭")

*코드 조각을 삽입할 선택한 코드 조각 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭*

![클릭 하 여 목록에서 관련 코드 조각 선택](aspnet-mvc-4-dependency-injection/_static/image24.png "클릭 하 여 목록에서 관련 코드 조각 선택")

*클릭 하 여 목록에서 관련 코드 조각 선택*
