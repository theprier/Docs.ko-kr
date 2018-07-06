---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: 자동화 된 단위 테스트 사용 | Microsoft Docs
author: microsoft
description: 12 단계는 NerdDinner 기능을 확인 하 고 제공 하는 안심 하 고 변경 하는 자동화 된 단위 테스트 모음을 개발 하는 방법을 표시 하는 중...
ms.author: aspnetcontent
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 2247dc2e6d22cc0d5ddba97dfe6c7d2d1b0e49be
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37819412"
---
<a name="enable-automated-unit-testing"></a>자동화 된 단위 테스트를 사용 하도록 설정
====================
[Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 12 단계 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 12 단계는 NerdDinner 기능을 확인 하 고 안심 하 고 변경 하 고 나중에 응용 프로그램의 향상 된 기능을 제공 합니다.는 자동화 된 단위 테스트 모음을 개발 하는 방법을 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-12-unit-testing"></a>NerdDinner 12 단계: 단위 테스트

NerdDinner 하는 기능을 확인 하 고 안심 하 고 변경 하 고 나중에 응용 프로그램의 향상 된 기능을 제공 합니다.는 자동화 된 단위 테스트 모음을 개발 해 보겠습니다.

### <a name="why-unit-test"></a>단위 테스트 하는 이유는?

작업 하나 아침에 드라이브에서 작업 하는 응용 프로그램에 대 한 영감 갑자기 flash를 수 있습니다. 알게를 개선할 응용 프로그램 대폭 변경 구현할 수 있습니다. 코드 정리, 새 기능을 추가 하거나 버그를 수정 하는 리팩터링 수 있습니다.

컴퓨터에 도착할 때이 마주치는 문제는 – "safe는이 개선 하기 위해?" 경우에 어떻게 변경 의도 하지 않은 나 무언가 중단 되었습니까? 변경 간단할 및 구현 하는 데 몇 분 하지만 수동으로 모든 응용 프로그램 시나리오를 테스트 하는 데 시간이 걸리는 경우에 사용할 수 있습니다? 시나리오를 처리 해야 하 고 손상 된 응용 프로그램을 프로덕션으로 전환 되 될까요? 실제로 가치가 모든이 개선 어떻습니까?

자동화 된 단위 테스트는 응용 프로그램을 지속적으로 향상 시킬 수 있도록 안전망을 제공 하 고 방지할에서 작업 하는 코드를 두려워 수 있습니다. 자동화 된 테스트 기능을 사용 하면 – 자신 있게 코딩 하 여 개선할 수이 고, 그렇지 없습니다가 느낌 편리 하 게을 신속 하 게 확인 하는 것을 수행 하 합니다. 이러한 상황은 더 쉽게 유지 관리할 수 있는 솔루션을 만들고 수명이 긴-는 잠재 고객을 훨씬 더 높은 투자 수익률도 도움이 됩니다.

ASP.NET MVC Framework 쉽고 자연스럽 게 단위 테스트 응용 프로그램의 기능 수 있도록 합니다. 또한 기반된 테스트 우선 개발을 사용 하도록 설정 하는 테스트 기반 개발 (TDD) 워크플로를 수 있습니다.

### <a name="nerddinnertests-project"></a>NerdDinner.Tests Project

이 자습서의 시작 부분에서 NerdDinner 응용 프로그램을 만들었을 때 응용 프로그램 프로젝트와 함께 이동할 단위 테스트 프로젝트 만들기 하려고 하는지 여부를 묻는 대화 상자가 표시 된 것:

![](enable-automated-unit-testing/_static/image1.png)

"예, 단위 테스트 프로젝트 만들기" 라디오 단추 선택 됨-이 인해 솔루션에 추가 되 고 "NerdDinner.Tests" 프로젝트를 유지 하면서:

![](enable-automated-unit-testing/_static/image2.png)

NerdDinner.Tests 프로젝트 NerdDinner 응용 프로그램 프로젝트 어셈블리를 참조 하 고 응용 프로그램 기능을 확인 하는 자동화 된 테스트를 쉽게 추가할 수 있습니다.

### <a name="creating-unit-tests-for-our-dinner-model-class"></a>저녁 식사 모델 클래스에 대 한 단위 테스트 만들기

이 모델 계층을 빌드할 때 만든 Dinner 클래스를 확인 하는 NerdDinner.Tests 프로젝트에 일부 테스트를 추가 하겠습니다.

여기서 모델 관련 테스트를 배치 "Models" 라는 테스트 프로젝트 내에서 새 폴더를 만들어 시작 하겠습니다. 에서는 다음 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 합니다 **추가-&gt;새 테스트** 메뉴 명령입니다. "새 테스트 추가" 대화 상자가 표시 됩니다.

"단위 테스트"를 만들고 이름을 "DinnerTest.cs"를 선택 합니다.

![](enable-automated-unit-testing/_static/image3.png)

"확인" 단추를 클릭할 때 Visual Studio는 추가 (연) DinnerTest.cs 파일을 프로젝트:

![](enable-automated-unit-testing/_static/image4.png)

기본 Visual Studio 단위 테스트 템플릿을 다양 한 상용구 코드 양을 필자는 약간 복잡 하는 내에 있습니다. 보겠습니다 정리만 아래 코드를 포함 합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

위의 DinnerTest 클래스에 대 한 [TestClass] 특성 테스트 뿐만 아니라 선택적 테스트 초기화 및 정리 코드를 포함 하는 클래스로 식별 합니다. 내 테스트 [TestMethod] 특성에 있는 공용 메서드를 추가 하 여 정의할 수 있습니다.

다음은 두 개의 테스트 추가 Dinner 클래스를 실행 하는 첫 번째입니다. 첫 번째 테스트는 Dinner 유효 하지 않음을 올바르게 설정 되 고 모든 속성 없이 새 Dinner 만들어지는 경우를 확인 합니다. 두 번째 테스트는 저녁에 유효한 값으로 설정 된 모든 속성 우리의 Dinner 유효한 지 확인 합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

우리 테스트 이름 매우 명시적 (및 어느 정도 자세한 정보)는 위에서 알 수 있습니다. 수백 또는 수천 개의 작은 테스트를 만드는 얻게 될 수 있습니다 (특히 경우 test runner에서 오류의 목록을 조사 하 고) 각각의 동작과 의도 빠르게 확인할 수 있도록 하고자 하기 때문에이 수행 하는 합니다. 테스트 이름은 테스트 하는 기능을 따서 지어야 합니다. 사용할 위에 "명사\_해야\_동사" 명명 패턴입니다.

"Arrange, Act, Assert"는 의미 있는 패턴-테스트 "AAA"를 사용 하 여 테스트를 구성할 것:

- 테스트 하는 단위를 설정 정렬 합니다.
- Act: 단위 테스트를 실행 하 고 결과 캡처
- 동작을 확인 어설션 됩니다.

작성할 때는 개별 테스트를 방지 하려면 테스트 너무 많은 것입니다. 대신 각 테스트만는 단일 개념 (됩니다 실패 원인을 정확 하 게 훨씬 더 쉬움)를 확인 해야 합니다. 사용해 보고 어설션 문을 각 테스트에 대 한 단일 하나만 것이 좋습니다. 있는 경우 둘 이상의 어설션 문을 테스트 메서드에서는 모두에 사용 하는 동일한 개념을 테스트 해야 합니다. 의문이 있으면 다른 테스트를 확인 합니다.

### <a name="running-tests"></a>테스트 실행 중

Visual Studio 2008 Professional (및 이상 버전)에 IDE 내에서 Visual Studio 단위 테스트 프로젝트를 실행 하는 데 사용할 수 있는 기본 제공 test runner를 포함 합니다. 선택할 수는 **테스트-&gt;실행-&gt;솔루션의 모든 테스트** 모든 단위 테스트를 실행 하려면 메뉴 명령 (또는 유형 Ctrl R, A). 특정 테스트 클래스 또는 테스트 메서드 내에서는 커서를 배치 하 고 사용할 수 있습니다 또는 또는 합니다 **테스트-&gt;실행-&gt;현재 컨텍스트의 테스트** 단위 테스트의 하위 집합을 실행 하려면 메뉴 명령 (또는 형식 Ctrl R, T).

보겠습니다 DinnerTest 클래스 내에서는 커서를 배치 하 고 방금 정의한 두 실행 테스트 "Ctrl R, T"를 입력 합니다. 이 수행할 때 "테스트 결과" 창이 Visual Studio 내에서 나타나고 실행에 나열 된 테스트의 결과 살펴보겠습니다.

![](enable-automated-unit-testing/_static/image5.png)

*참고: VS 테스트 결과 창 클래스 이름 열 기본적으로에 나타나지 않습니다. 테스트 결과 창 내에서 마우스 오른쪽 단추로 클릭 하 고 열 추가/제거 메뉴 명령을 사용 하 여이 추가할 수 있습니다.*

두 개의 테스트를 실행 하 고 – 수와 초의 일부만 걸린 전달 둘 다 참조 합니다. 수 이제 이동 하 고 이러한 두 가지 도우미 메서드-IsUserHost() 및 Dinner 클래스에 추가한 IsUserRegisterd() – 설명 뿐만 아니라 특정 규칙 유효성 검사를 확인 하는 추가 테스트를 만들어 확장. 저녁 식사 클래스에 대 한 이러한 모든 테스트를 하지 되도록 훨씬 쉽고 안전 하 게 새 비즈니스 규칙 및 유효성 검사를 나중에 추가 합니다. 저녁을를 새 규칙 논리를 추가 하 고 시간 (초) 내에서 이전 하는 논리 기능 중 하나 손상 되지 않은 것을 확인 수 있습니다.

어떻게 설명이 포함 된 테스트 이름을 사용 하 여 쉽게 파악한 다음 각 테스트를 확인 하는 것을 확인 합니다. 사용 하는 것이 좋습니다 합니다 **도구-&gt;옵션** 메뉴 명령, 여는 테스트 도구-&gt;테스트 실행 구성 화면 및 검사는 "실패 했거나 결과가 불충분 한 단위 테스트 결과 두 번 클릭 하면 표시 테스트의 실패 지점"확인란을 선택 합니다. 이렇게 하면 테스트 결과 창에서 오류를 두 번 클릭 하 고 어설션 실패를 즉시 이동할 수 있습니다.

### <a name="creating-dinnerscontroller-unit-tests"></a>DinnersController 단위 테스트 만들기

이제는 DinnersController 기능을 확인 하는 일부 단위 테스트를 만들어 보겠습니다. 에서는 테스트 프로젝트 내에서 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 하 여 시작 하 고 다음을 선택 합니다 **추가-&gt;새 테스트** 메뉴 명령입니다. "단위 테스트"를 만들어 "DinnersControllerTest.cs" 라는 이름을 지정 합니다.

DinnersController Details() 작업 메서드를 확인 하는 두 개의 테스트 메서드를 만들어 보겠습니다. 첫 번째 보기는 기존 Dinner 요청 될 때 반환 됩니다는 확인 합니다. 두 번째는 "NotFound" 뷰가 존재 하지 않는 Dinner 요청 될 때 반환 되는 확인할 것입니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

위의 코드 정리 컴파일합니다. 테스트를 실행 하면 하지만 모두 실패 합니다.

![](enable-automated-unit-testing/_static/image6.png)

오류 메시지를 보면 DinnersRepository 클래스를 데이터베이스에 연결할 수 없기 때문에 테스트에 실패 한 이유 되었는지 살펴보겠습니다. NerdDinner 응용 프로그램 연결 문자열을 사용 하 여는 \App 아래 있는 로컬 SQL Server Express 파일에는\_NerdDinner 응용 프로그램 프로젝트의 데이터 디렉터리입니다. NerdDinner.Tests 프로젝트를 컴파일하고 다른 디렉터리에 다음 응용 프로그램 프로젝트를 실행, 때문에 연결 문자열의 상대 경로 위치를 올바르지 않습니다.

우리 *없습니다* 테스트 프로젝트, SQL Express 데이터베이스 파일을 복사 하 여이 문제를 해결 하 고 테스트 프로젝트의 app.config에서를 적절 한 테스트 연결 문자열을 추가 합니다. 이 메일이 위의 테스트 차단이 해제 되 고 실행 합니다.

단위는 실제 데이터베이스를 사용 하 여 코드를 테스트 하지만 수반 챌린지 횟수입니다. 구체적으로는 다음과 같습니다.

- 단위 테스트의 실행 시간을 상당히 느려집니다. 자주 실행 하는 데 덜 발생할 가능성도 테스트를 실행 하는 데 걸리는 더 이상. 이상적으로 (초) –에서 실행을 하 게 할 것으로 프로젝트를 컴파일로 자연스럽 게 수 있으려면 단위 테스트 해야 합니다.
- 테스트 내에서 설정 및 정리 논리가 복잡 하다. 각 단위 테스트 격리 하 고 (부작용 이나 종속성)와 서로 독립적이 되도록 해야 합니다. 실제 데이터베이스에 대해 작업 하는 경우 상태에 주의 해야 하 고 테스트 사이의 다시 설정 해야 합니다.

이러한 문제를 해결 하 고 테스트를 사용 하 여 실제 데이터베이스를 사용할 필요가 없도록 하는 데 도움이 되는 "종속성 주입" 이라고 하는 디자인 패턴을 살펴보겠습니다.

### <a name="dependency-injection"></a>종속성 주입

지금 바로 DinnersController는 "밀접 하 게" DinnerRepository 클래스입니다. "결합"은 여기서 클래스를 명시적으로 다른는 클래스를 사용 하기 위해서는 상황을 말합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

DinnerRepository 클래스는 데이터베이스에 대 한 액세스를 필요로 하므로 DinnersController 클래스 긴밀 하 게 결합 된 종속성을 테스트할 DinnersController 작업 메서드에 대 한 주문 데이터베이스에 필요한 DinnerRepository 끝에 있습니다.

이 문제를 해결 방법은 종속성 (예: 데이터 액세스를 제공 하는 저장소 클래스)을 사용 하는 클래스 내에서 더 이상 암시적으로 생성 되는 위치는 "종속성 주입" – 이라고 하는 디자인 패턴을 사용 하 여 가져올 수 없습니다. 대신 종속성 명시적으로 전달할 수 사용 하는 클래스에 생성자 인수를 사용 하 여 합니다. 종속성 인터페이스를 사용 하 여 정의 되 면 다음 유연성이 단위 테스트 시나리오에 대 한 "가짜" 종속성 구현에 전달 합니다. 데이터베이스에 대 한 액세스를 실제로 필요 하지 않은 테스트 특정 종속성 구현을 만들 수 있습니다.

이 실행 중인 확인 하려면이 DinnersController 사용한 종속성 주입을 구현 해 보겠습니다.

#### <a name="extracting-an-idinnerrepository-interface"></a>IDinnerRepository 인터페이스 추출

첫 번째 단계는 컨트롤러를 검색 하 고 Dinners 업데이트 필요 리포지토리 계약을 캡슐화 하는 새 IDinnerRepository 인터페이스를 만들 수 있습니다.

\Models 폴더를 마우스 오른쪽 단추로 클릭 한 다음 선택 하면이 인터페이스 계약을 수동으로 정의할 수 있습니다 합니다 **추가-&gt;새 항목** 메뉴 명령 및 IDinnerRepository.cs 라는 새 인터페이스를 작성 합니다.

또는 수 리팩터링 도구 Visual Studio Professional에 기본 제공 (및 이상 버전)에 자동으로 추출을 사용 하 고 기존 DinnerRepository 클래스에서 한 인터페이스를 만듭니다. VS를 사용 하 여이 인터페이스를 추출 하려면 단순히 DinnerRepository 클래스, 텍스트 편집기에서 커서 다음 마우스 오른쪽 단추로 클릭을 선택 합니다 **리팩터링-&gt;인터페이스 추출** 메뉴 명령:

![](enable-automated-unit-testing/_static/image7.png)

"인터페이스 추출" 대화 상자가 시작 되 고 만들려면 인터페이스의 이름을 묻는 주세요. IDinnerRepository 기본값으로 설정 하 고 인터페이스에 추가할 기존 DinnerRepository 클래스에서 모든 공용 메서드를 자동으로 선택 합니다.

![](enable-automated-unit-testing/_static/image8.png)

"확인" 단추를 클릭 하는 경우 Visual Studio는 응용 프로그램에 새 IDinnerRepository 인터페이스를 추가 합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

및 기존 DinnerRepository 클래스 인터페이스를 구현 하 고 업데이트 됩니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a>생성자 주입을 지원 하도록 업데이트 DinnersController

이제 새 인터페이스를 사용 하는 DinnersController 클래스를 업데이트 됩니다.

현재 DinnersController 하드 코드는 해당 "dinnerRepository" 필드는 항상 DinnerRepository 클래스:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

에서는 DinnerRepository 대신 IDinnerRepository 형식의 "dinnerRepository" 필드는 되도록 변경 됩니다. 다음 두 명의 공용 DinnersController 생성자 추가 하겠습니다. 생성자 중 하나는 IDinnerRepository를 인수로 전달할 수 있습니다. 다른 하나는 기존 DinnerRepository 구현 하는 기본 생성자:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

기본적으로 ASP.NET MVC 컨트롤러 클래스 기본 생성자를 사용 하 여을 만들기 때문에 런타임 시이 DinnersController DinnerRepository 클래스를 사용 하 여 데이터 액세스를 수행 하려면 계속 됩니다.

이제 매개 변수 생성자를 사용 하 "는 가짜" dinner 저장소 구현에서 전달할 그러나 단위 테스트를 업데이트할 수 있습니다. 이 "가짜" dinner 리포지토리 실제 데이터베이스에 대 한 액세스를 필요 하지 않습니다 및 대신 메모리에 샘플 데이터를 사용 합니다.

#### <a name="creating-the-fakedinnerrepository-class"></a>FakeDinnerRepository 클래스 만들기

FakeDinnerRepository 클래스를 만들어 보겠습니다.

에서는 NerdDinner.Tests 프로젝트 내에서 "Fakes" 디렉터리를 만들어 시작 하 고 새 FakeDinnerRepository 클래스를 추가 합니다 (선택한 폴더를 마우스 오른쪽 단추로 클릭 **추가-&gt;새 클래스**):

![](enable-automated-unit-testing/_static/image9.png)

FakeDinnerRepository 클래스 IDinnerRepository 인터페이스를 구현 하는 코드를 업데이트 됩니다. 그런 다음에서 마우스 오른쪽 단추로 클릭 하 고 "인터페이스 구현 IDinnerRepository" 상황에 맞는 메뉴 명령을 선택 수 했습니다.

![](enable-automated-unit-testing/_static/image10.png)

이렇게 하면 기본적으로 "없애는" 구현 된 FakeDinnerRepository 클래스를 자동으로 추가 IDinnerRepository 인터페이스 멤버의 모든 Visual Studio:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

메모리 내 목록으로 작동 하는 FakeDinnerRepository 구현을 다음 업데이트할 수 있습니다&lt;Dinner&gt; 생성자 인수를 전달 하는 컬렉션:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

이제 데이터베이스에 필요 하지 않으며 수 Dinner 개체는 메모리 내 목록 대신 근무 하는 가짜 IDinnerRepository 구현을 했습니다.

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a>단위 테스트는 FakeDinnerRepository 사용

실패 한 이전 데이터베이스를 사용할 수 없는 DinnersController 단위 테스트를 다시 살펴보겠습니다. 테스트 메서드를 아래 코드를 사용 하 여 DinnersController 샘플 메모리 Dinner 데이터로 채울 FakeDinnerRepository를 사용 하 여 업데이트할 수 있습니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

고 이제 이러한 테스트를 실행 하는 경우 모두 전달 합니다.

![](enable-automated-unit-testing/_static/image11.png)

무엇을 실행 하려면 두 번째의 일부만 수행 하며 모든 복잡 한 설치/정리 논리가 필요 하지 않습니다. 단위 테스트 (만들기, 업데이트 및 삭제 페이징, 세부 정보를 포함 하 여 나열) DinnersController 작업 메서드 코드의 모든 실제 데이터베이스에 연결할 필요 없이 이제 수 있습니다.

| **쪽 항목: 종속성 주입 프레임 워크** |
| --- |
| 정상적으로 작동 하지만 종속성의 수를 관리 하기 어렵게 할 수 있는데요 수동 종속성 주입 (예: 위의 기꺼이)를 수행 하 고 응용 프로그램의 구성 요소를 늘립니다. 여러 종속성 주입 프레임 워크는 더 많은 종속성 관리 유연성을 제공 하는 데 도움이 되는.NET에 존재 합니다. 라고도 "Inversion of Control" (IoC) 컨테이너에 이러한 프레임 워크를 지정 하 고 (가장 자주 사용 하 여 런타임에 생성자 주입 개체 종속성을 전달 하기 위한 구성 지원 추가 수준을 사용할 수 있는 메커니즘 제공 ). 일부 더 인기 있는 OSS 종속성 주입.NET의 IOC 프레임 워크를 포함 하는 /: AutoFac "," Ninject "," Spring.NET "," StructureMap과 "및" Windsor입니다. ASP.NET MVC 확장성 개발자의 해상도 컨트롤러의 인스턴스화를 참여할 수 있도록 하 고 종속성 주입을 사용 하도록 설정 하는 Api 노출 / IoC 프레임 워크가이 프로세스 내에서 완전히 통합 될 수 있습니다. DI/IOC 프레임 워크를 사용 하 여 것도 허용를 고를 DinnerRepositorys 간의 결합을 완전히 제거는 우리의 DinnersController –에서 기본 생성자를 제거 합니다. 종속성 주입 사용 하지 않으므로 / NerdDinner 응용 프로그램을 사용 하 여 IOC 프레임 워크입니다. 하지만 것 NerdDinner 코드 베이스 및 기능 증가 하는 경우 향후 고려할 수 있습니다. |

### <a name="creating-edit-action-unit-tests"></a>편집 작업 단위 테스트 만들기

이제는 DinnersController의 편집 기능을 확인 하는 일부 단위 테스트를 만들어 보겠습니다. HTTP GET 버전은 편집 작업을 테스트 하 여 시작 하겠습니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

유효한 dinner 요청 될 때 DinnerFormViewModel 개체에서 지 원하는 보기를가 렌더링 됨을 확인 하는 테스트를 만듭니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

테스트를 실행 하면 그러나에서는 확인할 편집 메서드 Dinner.IsHostedBy() 검사를 수행 하려면 User.Identity.Name 속성에 액세스 하는 경우 null 참조 예외가 throw 됩니다 때문에 실패 하는지 있습니다.

기본 컨트롤러 클래스에서 사용자 개체에서 로그인 한 사용자에 대 한 세부 정보를 캡슐화 하 고 런타임 시 컨트롤러를 만들 때 ASP.NET MVC에서 채워집니다. 웹 서버 환경 외부에서 DinnersController를 테스트 하는 사용자 개체가 설정 되지 않습니다 (따라서 null 참조 예외).

### <a name="mocking-the-useridentityname-property"></a>모의 User.Identity.Name 속성

모의 프레임 워크는 테스트를 동적으로 가짜 버전의 테스트를 지 원하는 종속 개체를 만들고 사용 하 여 보다 쉽게 확인 합니다. 예를 들어, 우리의 DinnersController 시뮬레이션 된 사용자 이름을 조회 하는 데 사용할 수 있는 사용자 개체를 동적으로 만들려면 편집 작업 테스트에서 모의 프레임 워크를 사용할 수 있습니다. 테스트를 실행 하는 경우 throw 되는 null 참조를 피해 야 합니다.

많은.NET 모의 프레임 워크는 ASP.NET MVC를 사용 하 여 사용할 수 있습니다 (여기의 목록을 볼 수 있습니다: [ http://www.mockframeworks.com/ ](http://www.mockframeworks.com/)). 모의 프레임 워크 "Moq" 이라는 오픈 소스를 사용 하 여 NerdDinner 응용 프로그램 테스트를 위해 다운로드 가능한 무료에서 [ http://www.mockframeworks.com/moq ](http://www.mockframeworks.com/moq)합니다.

다운로드 한 후 추가한 참조일 NerdDinner.Tests 프로젝트에서 Moq.dll 어셈블리:

![](enable-automated-unit-testing/_static/image12.png)

그런 다음 사용자 이름 및 매개 변수를 변수로 DinnersController 인스턴스에서 User.Identity.Name 속성을 "모의" 개체를 테스트 클래스 "CreateDinnersControllerAs(username)" 도우미 메서드를 추가 하겠습니다 했습니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

위의 Moq (사용자, 요청, 응답 및 세션 같은 런타임 개체를 노출 하는 컨트롤러 클래스 넘어갑니다 ASP.NET MVC를 임) ControllerContext 개체 fakes는 모의 개체를 만들려면 사용 합니다. ControllerContext HttpContext.User.Identity.Name 속성 도우미 메서드에 전달 하는 사용자 이름 문자열을 반환 해야 함을 나타내려면 Mock의 "SetupGet" 메서드를 이라고 합니다.

임의 개수의 ControllerContext 속성 및 메서드를 모의 수 것입니다. 이 보여 주기 위해 Request.IsAuthenticated 속성 (아래 – 테스트에 실제로 필요 하지 않습니다는 아니라는 요청 속성을 모의 수 하는 방법을 보여 줍니다.) SetupGet() 호출도 추가 했습니다. 완료 될 때이 도우미 메서드는 반환 DinnersController를 ControllerContext mock 인스턴스에 할당 합니다.

이 도우미 메서드를 사용 하 여 다른 사용자를 포함 하는 편집 시나리오를 테스트 하는 단위 테스트를 작성할 수 있습니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

이제 테스트를 실행 하는 것을 전달 하 합니다.

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a>UpdateModel() 시나리오 테스트

편집 작업을 HTTP GET 버전을 포함 하는 테스트를 만들었습니다. 이제 편집 작업의 HTTP POST 버전을 확인 하는 몇 가지 테스트를 만들어 보겠습니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

이 작업 방법을 지원 하기 위한 흥미로운 새 테스트 시나리오는 컨트롤러 기본 클래스에서 UpdateModel() 도우미 메서드를 사용 합니다. 폼 게시 값 Dinner 개체 인스턴스를 바인딩할이 도우미 메서드를 사용 하는 것입니다.

다음은 양식 게시 UpdateModel() 도우미 메서드를 사용 하 여 값을 제공할 수 있는 방법을 보여 주는 두 가지 테스트입니다. 만들고 FormCollection 개체를 채워이 작업을 수행 하 고 컨트롤러에서 "ValueProvider" 속성에 할당 됩니다.

첫 번째 테스트는 성공적으로 저장 브라우저 리디렉션됩니다 상세 작업을 확인 합니다. 두 번째 테스트는 잘못 된 입력이 게시 되었을 때 작업을 다시 표시 되는 오류 메시지와 함께 다시 편집 보기를 확인 합니다.


[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a>테스트 요약

단위 테스트 컨트롤러 클래스에 관련 된 핵심 개념을 살펴보았습니다. 수백 개의 응용 프로그램의 동작을 확인 하는 간단한 테스트를 쉽게 만들려면 이러한 기법을 사용할 수 있습니다.

이 컨트롤러와 모델 테스트에는 실제 데이터베이스를 요구 하지 않으므로, 매우 빠르고 쉽게 실행할 수는 있습니다. 초를 수백 번의 자동화 된 테스트를 실행 하 고 즉시 수행한 변경 작업을 중단 여부에 대 한 피드백을 얻을 수 드리겠습니다. 안심 하 고 지속적으로 개선, 리팩터링 및 구체화 하는 응용 프로그램을 제공 하는 데 도움이 됩니다.

앞서 설명한 테스트를이 챕터에 – 마지막 항목으로 테스트 것 때문이 아니라 개발 프로세스의 끝에 수행 해야 하지만! 반면, 사용자가 가능한 한 빨리 개발 프로세스 자동화 된 테스트를 작성 해야 합니다. 이렇게 하면 하므로 가져올 수 있도록 즉각적인 피드백을 개발할 때는 응용 프로그램의 사용 사례 시나리오를 신중 하 게 고려 하 고 안내 하는 응용 프로그램을 디자인 하는 데 도움이 됩니다. 계층화 및 염두에서 결합 정리.

책의 뒷부분에 나오는 장에 테스트 기반 개발 (TDD)와 ASP.NET MVC와 함께 사용 하는 방법을 설명 합니다. TDD는 결과 코드 만족 하는 테스트를 먼저 작성는 반복적인 코딩 습관입니다. TDD를 사용 하 여 구현 하려고 하는 기능을 확인 하는 테스트를 만들어 각 기능을 시작 합니다. 테스트를 명확 하 게 이해 해야 기능 및 작업으로 간주 되는 방법을 먼저는 단위를 작성 합니다. 테스트 작성은 실패 하는지 확인 한 후에 수행 하면 다음 테스트를 확인 하는 실제 기능을 구현 합니다. 기능 작업으로 간주 되는 방법의 사용 사례에 대 한 시간 생각 얼마간 있으므로 해야 요구 사항을 더 잘 이해 하 고 구현 하는 최선의 방법입니다. 구현 테스트를 다시 실행 하 고에 대 한 즉각적인 피드백을 받을 수를 사용 하 여 완료 되 면 여부 기능이 제대로 작동 합니다. TDD 10 장에서 자세히 설명 합니다.

### <a name="next-step"></a>다음 단계

주석 위로 일부 최종 줄 바꿈 합니다.

> [!div class="step-by-step"]
> [이전](use-ajax-to-implement-mapping-scenarios.md)
> [다음](nerddinner-wrap-up.md)
