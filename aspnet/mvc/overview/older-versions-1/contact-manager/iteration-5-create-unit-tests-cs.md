---
uid: mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-cs
title: '반복 #5-단위 테스트 만들기 (C#) | Microsoft Docs'
author: microsoft
description: 다섯 번째 반복에서에서는 쉽게 응용 프로그램 유지 관리 하 고 단위 테스트를 추가 하 여 수정 합니다. 데이터 모델 클래스를 모의 하 고 o에 대 한 단위 테스트를 빌드하는 중...
ms.author: aspnetcontent
ms.date: 02/20/2009
ms.assetid: 28ad8f80-b8a5-444e-b478-8b15a846060c
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-cs
msc.type: authoredcontent
ms.openlocfilehash: 0da88a67f788be211c4aa7b909106e9dab9960f3
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37806004"
---
<a name="iteration-5--create-unit-tests-c"></a>반복 #5-단위 테스트 만들기 (C#)
====================
[Microsoft](https://github.com/microsoft)

[코드 다운로드](iteration-5-create-unit-tests-cs/_static/contactmanager_5_cs1.zip)

> 다섯 번째 반복에서에서는 쉽게 응용 프로그램 유지 관리 하 고 단위 테스트를 추가 하 여 수정 합니다. 데이터 모델 클래스를 모의 하 고는 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 작성 합니다.


## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>연락처 관리 ASP.NET MVC 응용 프로그램을 작성 (C#)

이 시리즈의 자습서에서 전체 연락처 관리 응용을 프로그램 시작부터 완료를 빌드합니다. 연락처 관리자 응용 프로그램에 사용자의 목록을 포함 된 상점 연락처 정보-이름, 전화 번호 및 전자 메일 주소-할 수 있습니다.

여러 반복에 응용 프로그램을 빌드합니다. 각 반복에서 점진적으로 응용 프로그램을 개선 했습니다. 이렇게 여러 반복의 목표는 각 변경의 이유를 이해할 수 있습니다.

- 반복 #1-응용 프로그램을 만듭니다. 첫 번째 반복에서 연락처 관리자에서에서 만드는 가장 간단한 방법은 가능 합니다. 기본 데이터베이스 작업에 대 한 지원 추가: 만들기, 읽기, 업데이트 및 삭제 (CRUD).

- 반복 #2-보기 좋게 응용 프로그램을 확인 합니다. 이 반복에서 기본 ASP.NET MVC 보기 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.

- 반복 #3-양식 유효성 검사를 추가 합니다. 세 번째 반복에서는 기본 양식 유효성 검사를 추가합니다. 사용자를 방지할 수를 필요한 형식의 필드를 완료 하지 않고 폼을 제출 합니다. 또한 전자 메일 주소 및 전화 번호 유효성을 검사 합니다.

- 반복 #4-느슨하게 결합 된 응용 프로그램을 확인 합니다. 이 세 번째 반복에서는 활용 쉽게 유지 관리 하 고 연락처 관리자 응용 프로그램을 수정 하려면 몇 가지 소프트웨어 디자인 패턴입니다. 예를 들어, 리포지토리 패턴 및 종속성 주입 패턴을 사용 하 여 응용 프로그램을 리팩터링 했습니다.

- 반복 #5-단위 테스트를 만듭니다. 다섯 번째 반복에서에서는 쉽게 응용 프로그램 유지 관리 하 고 단위 테스트를 추가 하 여 수정 합니다. 데이터 모델 클래스를 모의 하 고는 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 작성 합니다.

- 반복 #6-테스트 중심 개발을 사용 합니다. 이 여섯 번째 반복에서는 추가 새로운 기능을 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대 한 코드를 작성 합니다. 이 반복에서는 메일 그룹을 추가합니다.

- 반복 #7 – Ajax 기능을 추가 합니다. 일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 Ajax에 대 한 지원을 추가 하 여 합니다.


## <a name="this-iteration"></a>이 반복

연락처 관리자 응용 프로그램의 이전 반복에서는 더 느슨하게 결합 되어야 하는 응용 프로그램을 리팩터링 했습니다. 응용 프로그램 고유한 컨트롤러, 서비스 및 저장소 계층을 구분 했습니다. 인터페이스를 통해 그 아래의 계층을 사용 하 여 각 계층 상호 작용합니다.

응용 프로그램을 더 쉽게 유지 관리 및 모니터링 하려면 응용 프로그램을 리팩터링 했습니다. 예를 들어, 새 데이터 액세스 기술을 사용 하 여, 필요한 경우 변경할 수 있습니다 단순히 리포지토리 계층 컨트롤러 또는 서비스 계층을 변경 하지 않고도 합니다. 느슨하게 연결 된 연락처 관리자를 만들어에서는 ve 변경한 응용 프로그램을 변경 하려면 복원 력이 더욱 높아집니다.

하지만 연락처 관리자 응용 프로그램에 새 기능을 추가 해야 하는 경우 어떻게 되나요? 또는 우리가 버그를 수정 하는 경우 어떻게 되나요? 싫은 제대로 입증 된 코드를 작성 하는 사실는 새 버그를 도입 될 위험이 생성 되는 코드를 터치 할 때마다 합니다.

예를 들어, 하루 세밀 하 게, 관리자에 게 하도록 요청할 수도 있습니다 연락처 관리자에 새 기능을 추가 합니다. 메일 그룹에 대 한 지원을 추가 하려고 합니다. 사용자가 해당 연락처를 친구, 비즈니스 등 그룹으로 구성 하도록 하려고 합니다.

이 새로운 기능을 구현 하려면 연락처 관리자 응용 프로그램의 세 계층을 모두 수정 해야 합니다. 컨트롤러, 서비스 계층 및 저장소에 새 기능을 추가 해야 합니다. 코드를 수정, 시작 하는 즉시 중단 하기 전에 했던 기능 위험이 있습니다.

이전 반복에서 수행한 것 처럼 별도 레이어로 응용 프로그램을 리팩터링 했습니다. 응용 프로그램의 나머지 부분을 건드리지 않고 전체 계층에 변경 내용을 수행할 수 있기 때문에 한 것 이었습니다. 그러나 계층 내에서 코드를 더 쉽게 유지 하 고 수정 하려는 경우 코드에 대 한 단위 테스트 만들기 해야 합니다.

사용할 단위 테스트에는 개별 코드 단위입니다. 코드의 이러한 단위는 전체 응용 프로그램 계층 보다 작습니다. 일반적으로 사용 하 여 단위 테스트 코드의 특정 메서드에서 예상 되는 방식으로 동작 하는지 여부를 확인 하십시오. 예를 들어 ContactManagerService 클래스에 의해 노출 CreateContact() 메서드에 대 한 단위 테스트를 만듭니다.

만 하는 응용 프로그램 작업에 대 한 단위 테스트 안전망을 선호합니다. 응용 프로그램에서 코드를 수정할 때마다 수정에 기존 기능이 중단 되는지 여부를 확인 하는 단위 테스트 집합을 실행할 수 있습니다. 단위 테스트 코드를 수정 하려면 안전 하 게 확인 합니다. 단위 테스트 복원 력을 코드의 모든 응용 프로그램에서 변경 합니다.

이 반복에서 연락처 관리자 응용 프로그램에 단위 테스트를 추가 했습니다. 이런 방식으로 다음 반복에 추가할 수 있습니다 연락처 그룹 응용 프로그램에 기존 기능이 망가질 걱정할 필요 없이 합니다.

> [!NOTE] 
> 
> 단위 테스트 프레임 워크 NUnit, xUnit.net, MbUnit 등 여러 가지가 있습니다. 이 자습서에서는 단위 테스트 프레임 워크 Visual Studio를 함께 사용 합니다. 그러나 이러한 대체 프레임 워크 중 하나 사용 간단 하 게 수 없습니다.


## <a name="what-gets-tested"></a>어떤 테스트를 가져옵니다.

완벽 한 환경에서 모든 코드 단위 테스트에서 검사 수 됩니다. 완벽 한 세상에 완벽 한 안전망 해야 합니다. 응용 프로그램에서 코드 줄을 수정 하 고 알고 있는 즉시 단위 테스트를 실행 하 여 변경 내용을 기존 기능을 중단 하는지 여부를 수 있게 됩니다.

그러나에서는 인할 라이브 세상이 완벽 합니다. 연습에서는 단위 테스트를 작성 하는 경우, 비즈니스 논리 (예: 유효성 검사 논리)에 대 한 테스트 작성에 집중할 수 있습니다. 특히 있습니다 *하지* 데이터에 대 한 단위 테스트 작성 논리 또는 뷰 논리에 액세스 합니다.

유용 하려면 단위 테스트는 매우 신속 하 게 실행 해야 합니다. 쉽게 수백 또는 수천 응용 프로그램에 대 한 단위 테스트 축적 수 있습니다. 단위 테스트를 실행 하는 데 오래 걸릴 실행 방지할 수 있습니다. 즉, 장기 실행 단위 테스트는 매일 코딩 목적에 대 한 의미가 없습니다.

따라서 일반적으로 쓰지 않아도 데이터베이스 상호 작용 하는 코드에 대 한 단위 테스트 합니다. 라이브 데이터베이스에 대해 수백 개의 단위 테스트를 실행 합니다. 너무 느려질 수 있습니다. 대신, 데이터베이스를 모의 하 고 (설명 아래 데이터베이스를 모의) 모의 데이터베이스와 상호 작용 하는 코드를 작성 합니다.

비슷한 이유로, 일반적으로 쓰지 않아도 보기에 대 한 단위 테스트 합니다. 뷰를 테스트 하려면 웹 서버를 스핀업 해야 합니다. 웹 서버를 회전 비교적 속도가 느린 프로세스 이기 때문에 뷰에 대 한 단위 테스트를 만드는 권장 되지 않습니다.

보기에는 복잡 한 논리가 포함 된 경우 도우미 메서드로 이동 하는 논리를 고려해 야 합니다. 웹 서버를 포함 하지 않고도 실행 되는 도우미 메서드에 대 한 단위 테스트를 작성할 수 있습니다.

> [!NOTE] 
> 
> 데이터 액세스 논리에 대 한 테스트를 작성 하거나 뷰 논리는 좋지 않습니다 단위 테스트를 작성 하는 경우, 기능 구성 또는 통합 테스트 하는 경우에 이러한 테스트 매우 유용할 수 있습니다.


> [!NOTE] 
> 
> ASP.NET MVC Web Forms 뷰 엔진입니다. Web Forms 뷰 엔진을 웹 서버에 종속 된 동안 다른 뷰 엔진 되지 않을 수 있습니다.


## <a name="using-a-mock-object-framework"></a>모의 개체 프레임 워크를 사용 하 여

단위 테스트를 작성할 때 거의 항상 모의 개체 프레임 워크를 활용 해야 합니다. 모의 개체 프레임 워크를 사용 하면 응용 프로그램에서 모의 개체 및 클래스에 대 한 스텁을 만들 수 있습니다.

예를 들어을 모의 버전의 리포지토리 클래스를 생성 하는 모의 개체 프레임 워크를 사용할 수 있습니다. 이런 방식으로 단위 테스트에서 모의 리포지토리 클래스 실제 리포지토리 클래스 대신 사용할 수 있습니다. 모의 리포지토리를 사용 하 여 단위 테스트를 실행할 때 데이터베이스 코드를 실행 하지 않도록 수 있습니다.

Visual Studio 모의 개체 프레임 워크를 포함 하지 않습니다. 그러나 가지 여러 상용 및 오픈 소스에 대 한 모의 개체 프레임 워크.NET framework에서 사용할 수 있습니다.

1. Moq-이 프레임 워크는 오픈 소스 BSD 라이선스에서 사용할 수 있습니다. Moq에서 다운로드할 수 있습니다 [ https://code.google.com/p/moq/ ](https://code.google.com/p/moq/)합니다.
2. Rhino Mocks-이 프레임 워크는 오픈 소스 BSD 라이선스에서 사용할 수 있습니다. Rhino Mocks에서 다운로드할 수 있습니다 [ http://ayende.com/projects/rhino-mocks.aspx ](http://ayende.com/projects/rhino-mocks.aspx)합니다.
3. Typemock Isolator-이 파일은 상용 프레임 워크입니다. 평가판 버전을 다운로드할 수 있습니다 [ http://www.typemock.com/ ](http://www.typemock.com/)합니다.

이 자습서에서는 Moq를 사용 하기로 합니다. 그러나 Rhino Mocks를 간단 하 게 사용할 수 있습니다 또는 Mock를 만들려면 Typemock Isolator 연락처 관리자 응용 프로그램에 대 한 개체입니다.

Moq를 사용 하려면 먼저 다음 단계를 완료 해야 합니다.

1. .
2. 압축을 풀면 다운로드, 전에 확인 파일을 마우스 오른쪽 단추로 클릭 하 고 단추를 클릭 **차단 해제** (그림 1 참조).
3. 다운로드를 압축을 풉니다.
4. ContactManager.Tests 프로젝트의 참조 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 Moq 어셈블리에 대 한 참조를 추가 **참조 추가**합니다. 찾아보기 탭에서 Moq 압축을 푼 폴더로 이동 하 고 Moq.dll 어셈블리를 선택 합니다. 클릭 합니다 **확인** 단추입니다.
5. 다음이 단계를 완료 한 후 참조 폴더는 그림 2와 같습니다.


[![차단 해제 Moq](iteration-5-create-unit-tests-cs/_static/image1.jpg)](iteration-5-create-unit-tests-cs/_static/image1.png)

**그림 01**: 차단 해제 Moq ([큰 이미지를 보려면 클릭](iteration-5-create-unit-tests-cs/_static/image2.png))


[![Moq를 추가한 후 참조](iteration-5-create-unit-tests-cs/_static/image2.jpg)](iteration-5-create-unit-tests-cs/_static/image3.png)

**그림 02**: Moq를 추가한 후 참조 ([큰 이미지를 보려면 클릭](iteration-5-create-unit-tests-cs/_static/image4.png))


## <a name="creating-unit-tests-for-the-service-layer"></a>서비스 계층에 대 한 단위 테스트 만들기

이 연락처 관리자 응용 프로그램의 서비스 계층에 대 한 단위 테스트 집합을 만들어 시작 s 수 있습니다. 이 유효성 검사 논리를 확인 하려면 이러한 테스트를 사용 하겠습니다.

ContactManager.Tests 프로젝트의 Models 라는 새 폴더를 만듭니다. 다음으로 Models 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가, 새 테스트**합니다. 합니다 **새 테스트 추가** 그림 3 에서처럼 대화 상자가 나타납니다. 선택 합니다 **단위 테스트** 템플릿 ContactManagerServiceTest.cs 새 테스트 이름을 지정 합니다. 클릭 합니다 **확인** 테스트 프로젝트에 새 테스트를 추가 하려면 단추입니다.

> [!NOTE] 
> 
> 일반적으로 ASP.NET MVC 프로젝트의 폴더 구조와 일치 하도록 테스트 프로젝트의 폴더 구조를 해야 합니다. 예를 들어 컨트롤러 폴더는 Models 폴더에서 모델 테스트에 테스트 컨트롤러를 배치 및 등입니다.


[![Models\ContactManagerServiceTest.cs](iteration-5-create-unit-tests-cs/_static/image3.jpg)](iteration-5-create-unit-tests-cs/_static/image5.png)

**그림 03**: Models\ContactManagerServiceTest.cs ([큰 이미지를 보려면 클릭](iteration-5-create-unit-tests-cs/_static/image6.png))


처음에 ContactManagerService 클래스에 의해 노출 CreateContact() 메서드를 테스트 하려고 합니다. 다음 5 개의 테스트를 만듭니다.

- CreateContact()-테스트는 CreateContact() 유효한 연락처를 메서드에 전달 되 면 true를 반환 합니다.
- CreateContactRequiredFirstName()-오류 메시지가 모델 상태 때 누락 된 이름을 가진 연락처 추가 되어 있는지 테스트 CreateContact() 메서드에 전달 됩니다.
- CreateContactRequredLastName()-오류 메시지가 모델 상태 때 누락 된 성 가진 연락처를 추가 되어 있는지 테스트 CreateContact() 메서드에 전달 됩니다.
- CreateContactInvalidPhone()-오류 메시지가 모델 상태 때 잘못 된 전화 번호를 사용 하 여 연락처를 추가 되어 있는지 테스트 CreateContact() 메서드에 전달 됩니다.
- CreateContactInvalidEmail()-오류 메시지가 모델 상태 때 잘못 된 전자 메일 주소를 사용 하 여 연락처를 추가 되어 있는지 테스트 CreateContact() 메서드에 전달 됩니다...

첫 번째 테스트는 유효한 연락처를 유효성 검사 오류를 생성 하지 않는지 확인 합니다. 남은 테스트 각 유효성 검사 규칙을 확인합니다.

이러한 테스트에 대 한 코드는 목록 1에 포함 됩니다.

**Listing 1 - Models\ContactManagerServiceTest.cs**

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample1.cs)]


목록 1에서 Contact 클래스를 사용 하기 때문에 테스트 프로젝트에 Microsoft Entity Framework에 대 한 참조를 추가 해야 합니다. System.Data.Entity 어셈블리에 대 한 참조를 추가 합니다.


목록 1 [TestInitialize] 특성으로 데코 레이트 된 initialize () 메서드가 포함 되어 있습니다. 이 메서드는 각 단위 테스트를 실행 하기 전에 자동으로 호출 됩니다 (5 번 호출할 각 단위 테스트의 바로 앞). Initialize () 메서드 코드의 다음 줄을 사용 하 여 모의 리포지토리를 만듭니다.

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample2.cs)]

이 코드 줄 IContactManagerRepository 인터페이스에서 모의 리포지토리를 생성 하려면 Moq 프레임 워크를 사용 합니다. 모의 리포지토리의 각 단위 테스트를 실행할 때 데이터베이스에 액세스를 방지 하려면 실제 EntityContactManagerRepository 대신 사용 됩니다. IContactManagerRepository 인터페이스의 메서드를 구현 하는 모의 리포지토리 하지만 메서드 don t 실제로 아무 것도 수행 합니다.

> [!NOTE] 
> 
> 간의 구분이 Moq 프레임 워크를 사용할 때 \_mockRepository 및 \_mockRepository.Object 합니다. 이전의 Mock 가리킵니다&lt;IContactManagerRepository&gt; 모의 리포지토리를 동작 하는 방법을 지정 하는 메서드를 포함 하는 클래스입니다. 후자는 IContactManagerRepository 인터페이스를 구현 하는 실제 모의 리포지토리를 참조 합니다.


모의 리포지토리 ContactManagerService 클래스의 인스턴스를 만들 때 initialize () 메서드에서 사용 됩니다. 모든 개별 단위 테스트를 ContactManagerService 클래스의이 인스턴스를 사용합니다.

목록 1 각 단위 테스트에 해당 하는 5 개의 메서드를 포함 합니다. 이러한 각 메서드 [TestMethod] 특성으로 데코레이팅됩니다. 단위 테스트를 실행 하면이 특성을 가진 모든 메서드 호출 됩니다. 즉, [TestMethod] 특성으로 데코 레이트 된 모든 메서드는 단위 테스트.

CreateContact(), 명명 된 첫 번째 단위 테스트를 연락처 클래스의 유효한 인스턴스 메서드에 전달 되 면 CreateContact() 호출 값이 true 반환 하는지 확인 합니다. 테스트는 Contact 클래스의 인스턴스를 만들고 CreateContact() 메서드를 호출 하며 CreateContact() 값이 true를 반환 하는지 확인 합니다.

남은 테스트 확인 잘못 된 연락처를 CreateContact() 메서드를 호출 하는 경우 다음 메서드에서 false가 반환 한 예상된 유효성 검사 오류 메시지가 모델 상태에 추가 됩니다. 예를 들어 CreateContactRequiredFirstName() 테스트 FirstName 속성에 대해 빈 문자열을 사용 하 여 연락처 클래스의 인스턴스를 만듭니다. 다음으로, CreateContact() 메서드는 잘못 된 연락처를 사용 하 여 호출 됩니다. 마지막으로 테스트 확인 CreateContact() false를 반환 하 고 모델 상태에 필요한 유효성 검사 오류 메시지를 "이름은 필수입니다."

메뉴 옵션을 선택 하 여 목록 1에서 단위 테스트를 실행할 수 있습니다 **테스트를 실행 하 고 솔루션 (CTRL + R, A)의 모든 테스트**합니다. 테스트 결과 창에서 테스트의 결과가 표시 됩니다 (그림 4 참조).


[![테스트 결과](iteration-5-create-unit-tests-cs/_static/image4.jpg)](iteration-5-create-unit-tests-cs/_static/image7.png)

**그림 04**: 테스트 결과 ([큰 이미지를 보려면 클릭](iteration-5-create-unit-tests-cs/_static/image8.png))


## <a name="creating-unit-tests-for-controllers"></a>컨트롤러에 대 한 단위 테스트 만들기

ASP.NETMVC 응용 프로그램의 사용자 상호 작용 흐름을 제어 합니다. 컨트롤러를 테스트할 때는 컨트롤러 오른쪽 작업 결과 및 뷰 데이터를 반환 하는지 여부를 테스트 하려고 합니다. 또한 하려는 컨트롤러를 예상 하는 방식으로 모델 클래스와 상호 작용 하는지 여부를 테스트 합니다.

예를 들어 목록 2 create () 메서드 담당자 컨트롤러에 대 한 두 개의 단위 테스트를 포함 합니다. 인덱스 작업 create () 메서드 리디렉션됩니다 유효한 연락처를 create () 메서드에 전달 되 면 첫 번째 단위 테스트는 있는지 확인 합니다. 즉, 유효한 연락처를 전달 하는 경우 create () 메서드는 인덱스 작업을 나타내는 RedirectToRouteResult 반환 해야 합니다.

T 컨트롤러 계층을 테스트 하는 경우 ContactManager 서비스 계층을 테스트 하려는 하지 것입니다. 따라서에서는 모의 Initialize 메서드에 다음 코드를 사용 하 여 서비스 계층:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample3.cs)]

CreateValidContact() 단위 테스트에서에서는 모의 서비스 계층의 다음 줄의 코드로 CreateContact() 메서드 호출의 동작:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample4.cs)]

이 코드 줄 하면 모의 ContactManager 서비스가 해당 CreateContact() 메서드가 호출 되 면 true를 반환 합니다. 서비스 계층을 모의에서는 서비스 계층에서 모든 코드를 실행 하지 않고도 컨트롤러의 동작을 테스트할 수 있습니다.

두 번째 단위 테스트는 잘못 된 연락처를 메서드에 전달 될 때 create () 작업 만들기 뷰를 반환 하는지 확인 합니다. 서비스 계층 CreateContact() 메서드 코드의 다음 줄을 사용 하 여 값 false를 반환 하면:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample5.cs)]

Create () 메서드를 의도 한 대로 동작 하는 경우 서비스 계층 값 false를 반환 하는 경우 Create view를 반환 해야 하 합니다. 이런 방식으로 컨트롤러 뷰 만들기에서에서 유효성 검사 오류 메시지를 표시할 수 있고 사용자는 잘못 된 연락처 속성을 수정할 수 있는 기회입니다.


컨트롤러에 대 한 단위 테스트를 빌드 하려는 경우 다음 해야 컨트롤러 작업에서 명시적 보기 이름을 반환 합니다. 예를 들어, 다음과 같은 뷰를 반환 하지 않습니다.

View();를 반환 합니다.

대신, 다음과 같은 보기를 반환 합니다.

View("Create");를 반환 합니다.

없는 경우 명시적 보기를 반환 하는 경우 ViewResult.ViewName 속성이 빈 문자열을 반환 합니다.


**2-Controllers\ContactControllerTest.cs 나열**

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample6.cs)]

## <a name="summary"></a>요약

이 반복에서 연락처 관리자 응용 프로그램에 대 한 단위 테스트 생성 합니다. 언제 든 지 응용 프로그램 것으로 예상 하는 방식으로 계속 작동 하는지 확인 하려면 이러한 단위 테스트를 실행할 수 있습니다. 단위 테스트를 나중에 응용 프로그램을 안전 하 게 수정할 수 있어 응용 프로그램에 대 한 안전망으로 작동 합니다.

두 개의 단위 테스트 집합을 만들었습니다. 첫째, 유효성 검사 논리는 서비스 계층에 대 한 단위 테스트를 만들어 테스트 했습니다. 다음으로,이 흐름 제어 논리는 컨트롤러 계층에 대 한 단위 테스트를 만들어 테스트 했습니다. 이 서비스 계층을 테스트할 때에서는 별로 격리 된 테스트는 서비스 계층에 대 한이 저장소 계층에서이 저장소 계층을 모의 합니다. 컨트롤러 계층을 테스트할 때에서는 별로 격리 된 테스트는 컨트롤러 계층에 대 한 모의 서비스 계층입니다.

다음 반복에서는 수정 연락처 관리자 응용 프로그램에 게 문의 그룹을 지원 하도록 해당 합니다. 이 새로운 기능 테스트 기반 개발을 호출 하는 소프트웨어 디자인 프로세스를 사용 하 여 응용 프로그램을 추가 합니다.

> [!div class="step-by-step"]
> [이전](iteration-4-make-the-application-loosely-coupled-cs.md)
> [다음](iteration-6-use-test-driven-development-cs.md)
