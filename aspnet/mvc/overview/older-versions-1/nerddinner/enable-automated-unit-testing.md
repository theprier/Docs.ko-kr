---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: "Enable 단위 테스트를 자동화 된 | Microsoft Docs"
author: microsoft
description: "12 단계 우리의 업그레이드 되었으며 수정 기능을 확인 하 고 변경에 대 한 신뢰성을 제공 합니다.는 자동화 된 단위 테스트 모음을 개발 하는 방법을 보여 줍니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 1a4258054d90b2d5bcc06a63fb6f3b4673a4837d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="enable-automated-unit-testing"></a>자동화 된 단위 테스트를 사용 하도록 설정
====================
여 [Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 12 단계 ["업그레이드 되었으며 수정" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 하는 워크 쓰루는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 12 단계 우리의 업그레이드 되었으며 수정 기능을 확인 하 고 신뢰성 변경 하 고 나중에 응용 프로그램의 향상 된 기능을 제공 합니다.는 자동화 된 단위 테스트 모음을 개발 하는 방법을 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-12-unit-testing"></a>업그레이드 되었으며 수정 12 단계: 단위 테스트

우리의 업그레이드 되었으며 수정 기능을 확인 하 고 신뢰성 변경 하 고 나중에 응용 프로그램의 향상 된 기능을 제공 합니다.는 자동화 된 단위 테스트 모음을 개발 해 보겠습니다.

### <a name="why-unit-test"></a>단위 테스트 목적

작업 한 아침에 드라이브에서 작업 하는 응용 프로그램에 대 한 영감의 급격 한 플래시를 해야 합니다. 생각 되도록 응용 프로그램 획기적으로 더 나은 변경 구현할 수 있습니다. 코드를 정리, 새 기능을 추가 하거나 버그를 수정 하는 리팩터링 수도 있습니다.

이 컴퓨터에 도착할 때이 마주치 질문은 – "안전는 이러한 향상을 찾을 수 있도록?" 경우에 어떻게는 변경 내용을 의도 하지 않은 나 문제가 중단 되었습니까? 변경 내용을 단순 하 고 수동으로 응용 프로그램 시나리오의 모든 테스트 하는 데 시간이 걸리는 경우에 어떻게 하지만 구현 하려면 몇 분 정도만 소요? 손상된 된 응용 프로그램 생산을 개시를 시나리오를 포함 하 잊은 경우에 어떻게? 모든 활동 실제로 알아두는 것이 개선 어떻습니까?

자동화 된 단위 테스트는 지속적으로 응용 프로그램을 향상 시킬 수 있도록 안전망 제공 하 고 형식의 파일은 작업 중인 코드 되지 않게 수 있습니다. 자동화 된 기능을 사용 하면 – 하 여 정확 하 고 개선할 수도 그렇지 않으면 되지가 느낌 능숙 하는 권한을 부여 하면 신속 하 게 확인 하는 테스트 필요 수행 합니다. 또한 관리 되는 솔루션을 만들고 수명이 긴-투자 수익률을 훨씬 더 높거나 더는 잠재 고객을 지원할 합니다.

ASP.NET MVC 프레임 워크를 사용 하면 간편 하 고 단위 테스트 응용 프로그램의 기능을 합니다. 또한 테스트 기반 개발 (TDD) 워크플로를 기반으로 테스트 우선 개발을 수행할 수 있습니다.

### <a name="nerddinnertests-project"></a>NerdDinner.Tests 프로젝트

이 자습서의 시작 부분에서 업그레이드 되었으며 수정 응용 프로그램을 만들 때 응용 프로그램 프로젝트와 함께 이동 하려면 단위 테스트 프로젝트를 만들 주고자 있는지 여부를 묻는 대화 상자가 표시 된 했습니다.

![](enable-automated-unit-testing/_static/image1.png)

우리는 "예, 단위 테스트 프로젝트 만들기" 라디오 단추를 선택 – 했으며 솔루션에 추가 되 고 "NerdDinner.Tests" 프로젝트에 유지 됩니다.

![](enable-automated-unit-testing/_static/image2.png)

NerdDinner.Tests 프로젝트가 업그레이드 되었으며 수정 응용 프로그램 프로젝트 어셈블리를 참조 하 고 응용 프로그램 기능을 확인 하는 것을 자동화 된 테스트를 쉽게 추가할 수 있습니다.

### <a name="creating-unit-tests-for-our-dinner-model-class"></a>저녁 모델 클래스에 대 한 단위 테스트 만들기

모델 계층 우리의 구축 때 만든 Dinner 클래스를 확인 하는 당사의 NerdDinner.Tests 프로젝트에 일부 테스트를 추가 해 보겠습니다.

여기서이 정보를 배치 모델과 관련 된 테스트 "Models" 라는 우리의 테스트 프로젝트에 새 폴더를 만들어 시작 합니다. 다음 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 합니다 우리는 **추가-&gt;새 테스트** 메뉴 명령입니다. 이 "새 테스트 추가" 대화 상자를 표시 합니다.

"단위 테스트"을 만들고 이름을 "DinnerTest.cs"를 선택 합니다.

![](enable-automated-unit-testing/_static/image3.png)

"확인" 단추를 클릭 하는 경우 Visual Studio는 추가 (및 열) DinnerTest.cs 파일을 프로젝트:

![](enable-automated-unit-testing/_static/image4.png)

기본 Visual Studio 단위 테스트 템플릿을 찾으려면 약간 복잡 그 안에 보일 러 플레이트 코드 줄을 있습니다. 보겠습니다 정리 바로 아래에 있는 코드를 포함 하도록 합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

위의 DinnerTest 클래스에서 [TestClass] 특성 테스트도 선택적 테스트 초기화 및 정리 코드를 포함 하는 클래스로 식별 합니다. 내 테스트에 [TestMethod] 특성이 있는 공용 메서드를 추가 하 여 정의할 수 있습니다.

다음은 Dinner 클래스를 실행 하는 두 개의 테스트를 추가할 것 중 첫 번째 숫자입니다. 첫 번째 테스트 없이 모든 속성이 올바르게 설정 되 고 새 Dinner 만들어지면 우리의 Dinner 올바르지 않음을 확인 합니다. 두 번째 테스트는 저녁에 유효한 값으로 설정 된 모든 속성 우리의 Dinner 유효한 지 확인 합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

위의 예제 우리의 테스트 이름이 지 매우 명시적 (및 어느 정도 자세한 정보 표시). 수많은 소형 테스트를 만드는 생길 수 (특히 경우 test runner에서 실패의 목록에서 찾고)는 이러한 각 동작과 의도 신속 하 게 결정을 쉽게 확인 하고자 하기 때문에이 수행 하는 합니다. 테스트 이름에서 기능을 테스트 하 고 후 이름을 지정 해야 합니다. 사용 하 여 위에 "명사\_해야\_동사" 명명 패턴입니다.

"Arrange, Act, Assert"에 대 한 의미 있는 패턴 – 테스트 "AAA"를 사용 하 여 테스트 구성할 했습니다.

- 테스트 하는 단위를 설정 정렬 합니다.
- Act: 단위 테스트를 실행 한 결과
- 동작을 확인 어설션 됩니다.

작성할 때는 개별 테스트를 방지 하려면 테스트 너무 많은 것입니다. 대신 각 테스트만는 단일 (하는 개념은 훨씬 쉬워집니다 실패 원인을 정확 하 게)를 확인 해야 합니다. 시도 하 고 어설션 문을 각 테스트에 대 한 단일 하기만 하는 것이 좋습니다. 있는 경우 둘 이상의 어설션 테스트 메서드에서는 문을 모두 사용 하지 않을 같은 개념을 테스트할 수 있는지 확인 합니다. 의문이 있는 경우 다른 테스트를 확인 합니다.

### <a name="running-tests"></a>테스트 실행 중

Visual Studio 2008 Professional (및 이상 버전) IDE 내에서 Visual Studio 단위 테스트 프로젝트를 실행 하는 데 사용할 수 있는 기본 제공 test runner를 포함 합니다. 선택할 수는 **테스트-&gt;실행-&gt;솔루션의 모든 테스트** 모든 단위 테스트를 실행 하려면 메뉴 명령 (또는 형식 Ctrl R, A). 특정 테스트 클래스 또는 테스트 메서드 내에서 커서의 위치를 사용할 수 있습니다 또는 또는 **테스트-&gt;실행-&gt;현재 컨텍스트의 테스트** 단위 테스트의 하위 집합을 실행 하려면 메뉴 명령 (또는 형식 Ctrl R, T).

보겠습니다 DinnerTest 클래스 내에서 커서의 위치를 지정 하 고 방금 정의한 두 실행 테스트에 "Ctrl R, T"를 입력 합니다. 수행 하는 경우이 "테스트 결과" 창 Visual Studio 내에서 나타나고 실행 내에서 나열 된 테스트의 결과 확인할 수 있습니다.

![](enable-automated-unit-testing/_static/image5.png)

*참고: VS 테스트 결과 창 기본적으로 클래스 이름 열을 표시 하지 않습니다. 테스트 결과 창 내에서 마우스 오른쪽 단추로 클릭 하 고 열 추가/제거 메뉴 명령을 사용 하 여이 추가할 수 있습니다.*

두 테스트를 실행 하 고 – 때 수 있습니다. 두 번째의 일부만 걸린 전달 모두 참조 합니다. म 수 이제와 특정 규칙 유효성 검사 확인으로 도우미 메서드 두 개와-IsUserHost() 및 Dinner 클래스에 추가한 IsUserRegisterd()-를 포함 하는 추가 테스트를 만들어이 확장 합니다. 저녁 클래스에 대 한 현재 위치에 이러한 모든 테스트를 포함 하면 훨씬 더 쉽고 안전 하 게 새 비즈니스 규칙 및 유효성 검사를 나중에 추가 합니다. 저녁에이 새 규칙 논리를 추가할 수 있으며 다음 몇 초 이내 우리의 이전 논리 기능 인해 발생 하지 않은 것을 확인 했습니다.

설명이 포함 된 테스트 이름을 사용 하 여 손쉽게 방법을 신속 하 게 각 테스트를 확인 하는 이해를 확인 합니다. 사용 하는 것이 좋습니다는 **도구-&gt;옵션** 메뉴 명령, 열기, 테스트 도구-&gt;테스트 실행 구성 화면 및 검사는 "실패 했거나 결과가 불충분 한 단위 테스트 결과 두 번 클릭 하면 표시 테스트에 오류 지점의"확인란을 선택 합니다. 이렇게 하면 테스트 결과 창에 오류를 두 번 클릭 하 고 어설션 실패로 바로 이동할 수 있습니다.

### <a name="creating-dinnerscontroller-unit-tests"></a>DinnersController 단위 테스트 만들기

이제 우리 DinnersController 기능을 확인 하는 일부 단위 테스트를 만들어 보겠습니다. 이 테스트 프로젝트 내에서 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 하 여 시작 알아보고 선택 하겠습니다는 **추가-&gt;새 테스트** 메뉴 명령입니다. "단위 테스트"를 만들 알아보고 "DinnersControllerTest.cs" 라는 이름을 지정 하겠습니다.

에 DinnersController Details() 동작 메서드를 확인 하는 두 테스트 메서드를 만들어 보겠습니다. 첫 번째는 기존 Dinner 요청 되는 뷰가 반환 되는 것을 확인 합니다. 두 번째는 존재 하지 않는 Dinner 요청 된 경우 "NotFound" 보기 반환 됩니다 확인할 것입니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

위의 코드 정리 컴파일합니다. 테스트를 실행 하면 하지만 모두 실패 합니다.

![](enable-automated-unit-testing/_static/image6.png)

오류 메시지를 보면 DinnersRepository 클래스는 데이터베이스에 연결할 수 없기 때문에 테스트에 실패 한 이유 했음을 보겠습니다. 업그레이드 되었으며 수정 응용 프로그램은 연결 문자열을 사용 하 여는 \App에서 거주 하는 로컬 SQL Server Express 파일에\_업그레이드 되었으며 수정 응용 프로그램 프로젝트의 데이터 디렉터리입니다. 우리의 NerdDinner.Tests 프로젝트를 컴파일하고 다른 디렉터리에서 다음 응용 프로그램 프로젝트 실행을 하기 때문에 연결 문자열의 상대 경로 위치 올바르지 않습니다.

우리 *수* 우리의 테스트 프로젝트에 SQL Express 데이터베이스 파일을 복사 하 여이 문제를 해결 하 고이 테스트 프로젝트의 App.config에를 적절 한 테스트 연결 문자열을 추가 합니다. 이 얻게 위의 테스트를 차단 해제 하 고 실행 합니다.

단위는 실제 데이터베이스를 사용 하 여 코드를 테스트 하지만 수 있도록 도와주는 많은 문제입니다. 구체적으로는 다음과 같습니다.

- 단위 테스트의 실행 시간을 훨씬 느려집니다. 자주 실행 하는 데는 사용할수록 테스트를 실행 하는 데 걸리는 오래 합니다. 단위 테스트 (초) –에서 실행할 수 있고 프로젝트 컴파일로 자연스럽 게으로 있습니다 사용할 수 있게 되기를 원하는 것이 가장 좋습니다.
- 이 테스트 내에서 설정 및 정리 논리를 복잡해 집니다. 각 단위 테스트를 격리 되 고 독립적 다른 (부작용 또는 종속성)을 사용 하는 것이 좋습니다. 실제 데이터베이스에 대해 작업 하는 경우 상태에 주의 해야 하 고 테스트 사이의 다시 설정 해야 합니다.

이러한 문제를 해결 하 고 실제 데이터베이스가 테스트를 사용할 필요가 없도록 하는 데 도움이 되는 "종속성 주입" 이라는 디자인 패턴을 살펴보겠습니다.

### <a name="dependency-injection"></a>종속성 주입

지금 바로 DinnersController "밀접 됩니다" DinnerRepository 클래스. "연결"은 여기서 클래스 명시적으로 다른 클래스 하기 위해 사용 작동 하는 상황을 말합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

DinnerRepository 클래스는 데이터베이스에 대 한 액세스를 필요로 하므로 밀접 하 게 결합 된 종속성 DinnersController 클래스에 테스트할 DinnersController 작업 메서드에 대 한 순서 대로 데이터베이스를 필요로 하는 상태가 DinnerRepository 됩니다.

방식 (예: 데이터 액세스를 제공 하는 저장소 클래스)의 종속성을 사용 하는 클래스 내에서 더 이상 암시적으로 생성 되는 위치는 "종속성 주입" – 이라는 디자인 패턴을 사용 하 여이 문제를 해결할 수 없습니다. 대신, 종속성 명시적으로 전달할 수 메트릭을 사용 하는 클래스에 생성자 인수를 사용 하 여 합니다. 종속성 인터페이스를 사용 하 여 정의 된 경우에서는 다음는 단위 테스트 시나리오에 대 한 "가짜" 종속성 구현을에 전달할 수 있습니다. 이 데이터베이스에 대 한 액세스를 실제로 필요 하지 않은 테스트 특정 종속성 구현을 만들 수 있습니다.

예를 보려면, 우리의 DinnersController 사용한 종속성 주입을 구현 해 보겠습니다.

#### <a name="extracting-an-idinnerrepository-interface"></a>IDinnerRepository 인터페이스 추출

첫 번째 단계를 검색 하 고 업데이트 Dinners 우리의 컨트롤러 필요 리포지토리 계약을 캡슐화 하는 새 IDinnerRepository 인터페이스를 만드는 것입니다.

\Models 폴더를 마우스 오른쪽 단추로 클릭 한 다음 선택 하 여 수동으로이 인터페이스 계약을 정의할 수 있습니다는 **추가-&gt;새 항목** 메뉴 명령과 IDinnerRepository.cs 라는 새 인터페이스를 작성 합니다.

또는 도구 Visual Studio Professional에 기본 제공 (및 이상 버전)를 자동으로 리팩터링 추출 사용 하 고 기존 DinnerRepository 클래스에서 해 인터페이스를 만들 수 우리 합니다. VS를 사용 하 여이 인터페이스를 추출 하려면 단순히 DinnerRepository 클래스에 텍스트 편집기에서 커서의 위치를 다음 마우스 오른쪽 단추로 클릭 선택 된 **리팩터링-&gt;인터페이스 추출** 메뉴 명령:

![](enable-automated-unit-testing/_static/image7.png)

"인터페이스 추출" 대화 상자를 시작 되 고 us를 만들려면 인터페이스의 이름에 대 한 메시지를 표시 합니다. IDinnerRepository이 기본값으로 설정 되며 모든 공용 메서드는 인터페이스에 추가 하 여 기존 DinnerRepository 클래스에 자동으로 선택 합니다.

![](enable-automated-unit-testing/_static/image8.png)

"확인" 단추를 클릭 하면 Visual Studio 응용 프로그램에 새 IDinnerRepository 인터페이스를 추가 합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

및 기존 DinnerRepository 클래스를 인터페이스를 구현 하도록 업데이트 됩니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a>DinnersController 생성자 삽입을 지원 하도록 업데이트

이제 DinnersController 클래스의 새로운 인터페이스를 업데이트 하는.

현재 DinnersController는 하드 코드 된 "dinnerRepository" 필드는 항상 DinnerRepository 클래스 이상이 되도록 합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

DinnerRepository 대신 IDinnerRepository 형식의 "dinnerRepository" 필드는 있도록 것 변경 합니다. 다음 두 명의 공용 DinnersController 생성자를 추가 합니다. 생성자 중 하나는 IDinnerRepository를 인수로 전달할 수 있습니다. 다른 하나는 우리의 기존 DinnerRepository 구현을 사용 하는 기본 생성자:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

기본적으로 ASP.NET MVC 컨트롤러 클래스 기본 생성자를 사용 하 여을 만들기 때문에 런타임에 우리의 DinnersController DinnerRepository 클래스를 사용 하 여 데이터 액세스를 수행 계속 됩니다.

이제 매개 변수 생성자를 사용 하는 "가짜" dinner 저장소 구현에 전달 하도록 단위 테스트에서는 하지만 업데이트할 수 있습니다. 이 "가짜" dinner 실제 데이터베이스에 액세스 하지 않아도 됩니다 리포지토리와 대신 메모리에 샘플 데이터를 사용 합니다.

#### <a name="creating-the-fakedinnerrepository-class"></a>FakeDinnerRepository 클래스 만들기

FakeDinnerRepository 클래스를 만들어 보겠습니다.

먼저 우리의 NerdDinner.Tests 프로젝트 내에서 "Fakes" 디렉터리를 만들어 알아보고 새 FakeDinnerRepository 클래스를 추가 하겠습니다 (폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가-&gt;새 클래스**):

![](enable-automated-unit-testing/_static/image9.png)

코드 FakeDinnerRepository 클래스 IDinnerRepository 인터페이스를 구현 있도록 업데이트 됩니다. 마우스 오른쪽 단추로 클릭 하 고 "인터페이스 구현 IDinnerRepository" 상황에 맞는 메뉴 명령 선택 다음 했습니다.

![](enable-automated-unit-testing/_static/image10.png)

이렇게 하면 Visual Studio IDinnerRepository 인터페이스 멤버의 모든 기본 "스텁" 구현과 함께 FakeDinnerRepository 클래스를 자동으로 추가 하려면:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

메모리 내 목록에서 작동 하도록 FakeDinnerRepository 구현을 업데이트할 수 있습니다&lt;Dinner&gt; 생성자 인수에 전달 되는 컬렉션:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

데이터베이스에 필요 하지 않으며 대신 Dinner 개체는 메모리에 목록이 해제 작업 수 하는 가짜 IDinnerRepository 구현을 했습니다.

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a>단위 테스트는 FakeDinnerRepository 사용

실패 한 이전 데이터베이스를 사용할 수 없는 DinnersController 단위 테스트에 다시 살펴보겠습니다. 아래 코드를 사용 하 여 DinnersController 샘플 메모리 Dinner 데이터로 채울 FakeDinnerRepository를 사용 하는 테스트 메서드를 업데이트할 수 있습니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

고 이제이 테스트 실행 하면 모두 통과 합니다.

![](enable-automated-unit-testing/_static/image11.png)

무엇 보다도를 실행 하려면 두 번째의 일부만 걸리고는 복잡 한 설치/정리 논리는 필요 하지 않습니다. 이제 단위 테스트 DinnersController 동작 메서드 코드 (만들기, 업데이트 및 삭제 페이징, 세부 정보를 포함 하 여 목록)의 모든 현재까지 실제 데이터베이스에 연결 하지 않고도 수 있습니다.

| **종속성 주입 프레임 워크 쪽 항목:** |
| --- |
| 정상적으로 작동 하지만 종속성의 수로 유지 하기 쉽다는 점 상태가 않는 수동 종속성 주입 (예: 위에서)를 수행 하 고 응용 프로그램의 구성 요소를 늘립니다. 여러 개의 종속성 주입 프레임 워크가 더 많은 종속성 관리 유연성을 제공 하는 데 도움이 되는.NET 존재 합니다. "Inversion of Control" (IoC) 컨테이너를이 라고도 함 이러한 프레임 워크를 지정 하 고 개체 (가장 자주 사용 하 여 런타임에 생성자 삽입에 종속성을 전달 하기 위한 구성 지원 추가 수준을 사용할 수 있는 메커니즘 제공 ). 일부 더 인기가 OSS 종속성 주입.net에서 프레임 워크 IOC /include: AutoFac "," Ninject "," Spring.NET "," StructureMap, "및" Windsor 합니다. ASP.NET MVC 확장성 Api 수 있도록 하는 해상도 및 컨트롤러의 인스턴스화에 참여 하는 개발자 및 종속성 주입이를 통해 노출 / IoC 프레임 워크가이 프로세스 내에서 완전히 통합 될 수 있습니다. DI/IOC 프레임 워크를 사용 하 여도 하면 기본 생성자는 DinnerRepositorys 간의 결합을 완전히 제거는 우리의 DinnersController –에서 제거할 수 있습니다. 종속성 삽입을 사용 하지 / 업그레이드 되었으며 수정 응용 프로그램으로 IOC 프레임 워크입니다. 하지만 업그레이드 되었으며 수정 코드 베이스 및 특성은 증가 하는 경우 미래를 위한 고려할 수 문제입니다. |

### <a name="creating-edit-action-unit-tests"></a>편집 작업 단위 테스트 만들기

이제는 DinnersController의 편집 기능을 확인 하는 일부 단위 테스트를 만들어 보겠습니다. HTTP GET 버전 우리의 편집 작업을 테스트 하 여 시작 합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

유효한 dinner가 요청 될 때 다시 DinnerFormViewModel 개체에서 지 원하는 보기가 렌더링 됨을 확인 하는 테스트를 만들겠습니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

테스트를 실행 하면 Edit 메서드 Dinner.IsHostedBy() 검사를 수행 하도록 User.Identity.Name 속성에 액세스 하는 경우 null 참조 예외가 throw 되는 실패 소요 됩니다 하지만 합니다.

컨트롤러의 기본 클래스에 사용자 개체에 로그인 한 사용자에 대 한 세부 정보를 캡슐화 하 고 런타임 시 컨트롤러를 만들 때 ASP.NET MVC에서 채워집니다. 웹 서버 환경 외부에서 DinnersController 테스트 하는, 때문에 사용자 개체 설정 되어 있지 않습니다 (따라서는 null 참조 예외가).

### <a name="mocking-the-useridentityname-property"></a>모의 User.Identity.Name 속성

모의 프레임 워크는 동적으로 가짜 버전의 종속 개체를 지 원하는 테스트를 만들고 사용 하 여 테스트를 보다 쉽게 확인 합니다. 예를 들어 동적으로 개체를 만들려면 사용자 우리의 DinnersController 시뮬레이션 된 사용자 이름을 조회 하는 데 사용할 수 있는 편집 작업 테스트에서 모의 프레임 워크를 사용할 수 있습니다. 이 테스트 실행 하면 throw 되는 null 참조를 피해 야 합니다.

많은.NET 모의 ASP.NET MVC와 함께 사용할 수 있는 프레임 워크는 (여기의 목록을 볼 수 있습니다: [http://www.mockframeworks.com/](http://www.mockframeworks.com/)). 모의 프레임 워크 "Moq"를 호출 하는 오픈 소스에서는 업그레이드 되었으며 수정 응용 프로그램 테스트를 위해 다운로드 가능한 무료에서 [http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq)합니다.

를 다운로드 한 후 Moq.dll 어셈블리에 NerdDinner.Tests 프로젝트에 대 한 참조를 추가 합니다 했습니다.

![](enable-automated-unit-testing/_static/image12.png)

"CreateDinnersControllerAs(username)" 도우미 메서드를 사용 하는 다음 매개 변수를 지정 하 고 있는 사용자 이름을 변수로 다음 "mocks" DinnersController 인스턴스에서 User.Identity.Name 속성에서는 테스트 클래스에 추가 합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

위에 Moq (사용자, 요청, 응답 및 세션 같은 런타임 개체를 노출 하는 컨트롤러 클래스에 전달 될 ASP.NET MVC를 즉) ControllerContext 개체 fakes 모의 개체를 만들려면 사용 합니다. ControllerContext에 HttpContext.User.Identity.Name 속성 म 도우미 메서드에 전달 된 사용자 이름 문자열을 반환 해야 함을 나타내기 위해 모의에 "SetupGet" 메서드를 호출 합니다.

म ControllerContext 속성 및 메서드의 여러를 모의 수 있습니다. 이 설명 하기 위해 Request.IsAuthenticated 속성 (아래 – 테스트에 대 한 실제로 필요 하지 않습니다는 하지만 요청 속성을 모의 수는 방법을 보여 줍니다. 수)에 대 한 SetupGet() 호출 또한 추가 했습니다. 완료 될 때 ControllerContext 모의의 인스턴스를 반환 하는 도우미 메서드 DinnersController 할당 합니다.

이제이 도우미 메서드를 사용 하 여 다른 사용자가 포함 하는 편집 시나리오를 테스트 하는 단위 테스트를 작성할 수 있습니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

이제 테스트 실행을 전달 하 합니다.

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a>테스트 UpdateModel() 시나리오

HTTP GET 버전 편집 작업을 포괄 하는 테스트 만들었습니다. 이제 편집 작업의 HTTP POST 버전을 확인 하는 몇 가지 테스트를 만들어 봅니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

이 작업 방법을 지원 하기에 대 한 흥미로운 새 테스트 시나리오는 해당 컨트롤러의 기본 클래스에 UpdateModel() 도우미 메서드를 사용 합니다. 폼 게시 값 Dinner 개체 인스턴스를 바인딩할이 도우미 메서드를 사용 하는 것입니다.

다음은 사용할 UpdateModel() 도우미 메서드에 대 한 값을 게시 하는 폼 제공 방법을 보여 주는 두 가지 테스트입니다. 컨트롤러에서 "ValueProvider" 속성에 할당 한 다음 알아보고 만들고 채워 FormCollection 개체를이 작업을 수행 하겠습니다.

첫 번째 테스트는 성공적으로 저장에는 브라우저가 리디렉션되 상세 작업을 확인 합니다. 두 번째 테스트는 잘못 된 입력이 게시 될 때 동작 하 여 표시 하 고 오류 메시지가 다시 편집 뷰를 확인 합니다.


[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a>래핑 테스트

설명한 단위 테스트 컨트롤러 클래스에 관련 된 핵심 개념입니다. 쉽게 수백 개의 응용 프로그램의 동작을 확인 하는 간단한 테스트를 만들 이러한 기법을 사용할 수 있습니다.

이 컨트롤러와 모델 테스트에는 실제 데이터베이스를 요구 하지 않으므로, 매우 빠르고 쉽게 실행할 수는 있습니다. (초)을 수백 대의 자동화 된 테스트를 실행 하 고 즉시 적용 한 변경 내용을 म 문제가 중단 하는지 여부에 대 한 피드백을 받을 수 됩니다. 지속적으로 개선을 리팩터링 하 고 응용 프로그램을 구체화할 신뢰성을 제공 하는 데 도움이 됩니다.

테스트 다룬 –이 장의 마지막 항목으로 것은 테스트 때문이 아니라 개발 프로세스의 끝에 수행 해야 하지만! 반대로 사용자가 가능한 한 빨리 개발 프로세스 자동화 된 테스트를 작성 해야 합니다. 이렇게 하면 되므로 가져올 수 있습니다 즉각적인 피드백을 개발할 때는 응용 프로그램의 사용 사례 시나리오에 대 한 면밀히 생각 하 고 안내해 응용 프로그램을 디자인 하는 데 도움이 됩니다. 계층화 고 염두에서 결합을 정리 합니다.

책에 이후 장의 테스트 기반 개발 (TDD) 및 ASP.NET MVC와 함께 사용 하는 방법을 설명 합니다. TDD는 먼저 작성 결과 코드를 만족 하는 테스트는 반복 코딩 방식은 합니다. TDD로 구현 하려고 하는 기능을 확인 하는 테스트를 만들어 각 기능을 시작 합니다. 단위 테스트 처음 사용 하는 경우 명확 하 게 이해 하는 기능과 작동 하도록 되어 어떻게를 작성 합니다. 테스트가 기록 됩니다 (및 실패 하는지 확인 한) 후에 수행 하면 다음 실제 테스트 확인 기능을 구현 합니다. 요구 사항을 더 잘 이해 해야 합니다 기능이 작동 하도록 되는 방법의 사용 사례에 대 한 시간 생각 얼마간 때문에를 구현 하는 가장 효율적인 방법은 합니다. -테스트를 다시 실행 하 고로 대 한 즉각적인 피드백을 받을 수 구현으로 완료 되 면 여부 기능이 제대로 작동 합니다. 장 10에서 더 TDD 설명 합니다.

### <a name="next-step"></a>다음 단계

메모를 몇 가지 최종 줄 바꿈 합니다.

>[!div class="step-by-step"]
[이전](use-ajax-to-implement-mapping-scenarios.md)
[다음](nerddinner-wrap-up.md)
