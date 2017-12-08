---
uid: mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-cs
title: "반복 #5 – 만들기 단위 테스트 (C#) | Microsoft Docs"
author: microsoft
description: "다섯 번째 반복에서 하도록 응용 프로그램이 쉽게 유지 관리 및 단위 테스트를 추가 하 여 수정 합니다. 데이터 모델 클래스를 모의 하 고 o에 대 한 단위 테스트 빌드 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: 28ad8f80-b8a5-444e-b478-8b15a846060c
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-cs
msc.type: authoredcontent
ms.openlocfilehash: f9b2d05ec8756d68f6bd2f387c85faf03abd167e
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="iteration-5--create-unit-tests-c"></a>반복 #5-단위 테스트를 만듭니다 (C#)
====================
여 [Microsoft](https://github.com/microsoft)

[코드 다운로드](iteration-5-create-unit-tests-cs/_static/contactmanager_5_cs1.zip)

> 다섯 번째 반복에서 하도록 응용 프로그램이 쉽게 유지 관리 및 단위 테스트를 추가 하 여 수정 합니다. 데이터 모델 클래스를 모의 하 고 우리의 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 작성 합니다.


## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>ASP.NET MVC 연락처 관리 응용 프로그램 (C#) 빌드

이 일련의 자습서에서는 전체 연락처 관리 응용을 프로그램의 시작 끝나기를 빌드합니다. 관리자에 게 문의 응용 프로그램을 사람 목록에 대 한 사용-이름, 전화 번호 및 전자 메일 주소-연락처 정보를 저장할 수 있습니다.

여러 반복을 통해에 응용 프로그램을 빌드합니다. 각 반복에서 점진적으로 응용 프로그램을 개선 했습니다. 이 여러 개의 반복 접근 방법의 목적은 각 변경의 이유를 이해 하는 데 사용할 수 있도록 하는 것입니다.

- 반복 #1-응용 프로그램을 만듭니다. 첫 번째 반복에서는 만듭니다 연락처 관리자에는 가장 간단한 방법은 가능한. 기본적인 데이터베이스 작업에 대 한 지원을 추가 하 여: 만들기, 읽기, 업데이트 및 삭제 (CRUD).

- 반복 #2-모양이 아닌 응용 프로그램을 확인 합니다. 이 반복에서 기본 ASP.NET MVC 뷰 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.

- 반복 #3-폼 유효성 검사를 추가 합니다. 세 번째 반복에서 기본적인 형태의 유효성 검사를 추가 했습니다. म 중이거나 사용자에서 필수 양식 필드를 완료 하지 않고 폼을 제출 합니다. 또한 전자 메일 주소, 전화 번호를 확인 합니다.

- 반복 #4-느슨하게 결합 된 응용 프로그램을 확인 합니다. 이 세 번째 반복에서 우리 활용 여러 가지 소프트웨어 디자인 패턴을 쉽게 유지 관리 하 고 않아 응용 프로그램을 수정 합니다. 예를 들어 리팩터링한 리포지토리 패턴 및 종속성 주입 패턴을 사용 하도록 응용 프로그램입니다.

- 반복 #5-단위 테스트를 만듭니다. 다섯 번째 반복에서 하도록 응용 프로그램이 쉽게 유지 관리 및 단위 테스트를 추가 하 여 수정 합니다. 데이터 모델 클래스를 모의 하 고 우리의 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 작성 합니다.

- 반복 6-테스트 기반 개발을 사용 합니다. 이 6 번째 반복에서에서는 새 기능을 추가할 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대해 코드를 작성 합니다. 이 반복 메일 그룹을 추가합니다.

- 반복 #7-Ajax 기능을 추가 합니다. 일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 ajax 지원을 추가 하 여 합니다.


## <a name="this-iteration"></a>이 반복

않아 응용 프로그램의 이전 반복의 응용 프로그램을 느슨하게 결합 될 리팩터링 했습니다. 에서는 응용 프로그램 고유 컨트롤러, 서비스 및 저장소 계층을 구분합니다. 각 계층은 인터페이스를 통해 그 아래의 계층 상호 작용합니다.

응용 프로그램을 더 쉽게 유지 관리 및 모니터링 하려면 응용 프로그램을 리팩터링 했습니다. 예를 들어 새 데이터 액세스 기술을 사용 하 여 필요한 경우 변경할 수 있습니다 단순히 리포지토리 계층 컨트롤러 또는 서비스 계층을 터치 하지 않고도 합니다. 느슨하게 결합 된 않아 함으로써 म 했습니다 만든 응용 프로그램을 변경 하려면 복원 성도 뛰어납니다.

그러나 않아 응용 프로그램에 새 기능을 추가 해야 할 때 어떻게 될까요? 또는 여기서는 버그를 해결 하면 어떻게 되나요? 코드 작성의 sad, 하지만 잘 검증 된 진리는 새 버그의 위험 생성 되는 코드를 터치 할 때마다는 됩니다.

예를 들어 하루 세밀 하 게, 관리자 요청 받을 수 Contact Manager에 새로운 기능을 추가할 수 있습니다. 원하는 메일 그룹에 대 한 지원을 추가할 수 있습니다. 연락처의 친구, 비즈니스, 등의 그룹으로 구성 하는 사용자가 사용할 수 있습니다. 하려고 합니다.

이 새로운 기능을 구현 하려면 않아 응용 프로그램의 모든 3 개의 계층을 수정 해야 합니다. 컨트롤러, 저장소 및 서비스 계층에 새 기능을 추가 해야 합니다. 코드를 수정을 시작 하는 즉시 이전에 작동 하는 기능을 손상 시 키 지 발생할 수 있습니다.

이전 반복에서와 같이 별도 계층으로 응용 프로그램을 리팩터링 한 것 이었습니다. 응용 프로그램의 나머지 부분을 터치 하지 않고 전체 계층을 변경할 수 있도록 하기 때문에 한 것 이었습니다. 그러나 계층 내에서 코드를 더 쉽게 유지 하 고 수정 하려는 경우 코드에 대 한 단위 테스트를 만들 해야 합니다.

통해 단위 테스트에 테스트 코드의 개별 단위. 코드의 이러한 단위는 전체 응용 프로그램 계층 보다 작습니다. 일반적으로 코드의 특정 메서드 있어야 하는 방식으로 작동 하는지 여부를 확인 하려면 단위 테스트를 사용 합니다. 예를 들어, 단위 테스트는 ContactManagerService 클래스에 의해 노출 되는 CreateContact() 메서드를 만듭니다.

정당한는 응용 프로그램 작업에 대 한 단위 테스트 같은 안전망입니다. 응용 프로그램에서 코드를 수정할 때마다 수정 기존 기능을 중단할지 여부를 확인 하려면 단위 테스트의 집합을 실행할 수 있습니다. 단위 테스트를 수정 해도 코드를 확인 합니다. 단위 테스트 확인 코드의 모든 응용 프로그램에서 변경 하려면 복원 성도 뛰어납니다.

이 반복에 않아 응용 프로그램에 단위 테스트 추가합니다. 이런 방식으로 다음 반복에 추가할 수 있습니다 메일 그룹 응용 프로그램을 기존 기능을 분리 하는 방법에 대 한 걱정 없이 합니다.

> [!NOTE] 
> 
> 단위 테스트 프레임 워크 NUnit, xUnit.net, MbUnit 등의 여러 가지가 있습니다. 이 자습서에서는 단위 테스트 프레임 워크 Visual Studio에 포함 된 사용 합니다. 하지만, 손쉽게 사용할 대체 이러한 프레임 워크 중 하나입니다.


## <a name="what-gets-tested"></a>테스트 내용을 가져옵니다.

완벽 한 상황에서 단위 테스트에서 검사 모든 코드는 합니다. 완벽 한 상황에서 완벽 한 안전망 해야 했습니다. 응용 프로그램의 코드 줄을 수정 하 고 알고 있는 즉시 단위 테스트를 실행 하 여 변경 내용을 기존 기능이 중단 여부 수 있게 됩니다.

그러나 우리 인할 라이브 이상적인 합니다. 연습에서는 단위 테스트를 작성 하는 경우, 비즈니스 논리 (예: 유효성 검사 논리)에 대 한 테스트를 작성에 집중 합니다. 특히, 있습니다 *없는* 데이터에 대 한 단위 테스트를 작성 논리 또는 뷰 논리에 액세스 합니다.

유용 하 게 되려면 단위 테스트는 매우 빠르게 실행 해야 합니다. 하면 쉽게 누적 될 수 있는 수백 또는 수천을 응용 프로그램에 대 한 단위 테스트 합니다. 단위 테스트를 실행 하는 데 오래 걸리거나 실행 방지할 수 있습니다. 즉, 장기 실행 단위 테스트는 코딩을 위한 일상적인 하는 데 사용할 수 없습니다.

이러한 이유로, 일반적으로 작성 하지 않는 데이터베이스와 상호 작용 하는 코드에 대 한 단위 테스트 합니다. 라이브 데이터베이스에 대해 수백 개의 단위 테스트를 실행 중인 너무 속도가 느려질 수 있습니다. 대신, 데이터베이스의 모의 알림 및 모의 (논의 아래의 데이터베이스를 모의) 데이터베이스와 상호 작용 하는 코드를 작성 합니다.

비슷한 이유로, 일반적으로 작성 하지 않는 뷰에 대 한 단위 테스트 합니다. 뷰를 테스트 하려면 웹 서버를 회전 시켜 해야 합니다. 웹 서버를 회전 상대적으로 속도가 느립니다 프로세스 이기 때문에 사용자 보기에 대 한 단위 테스트를 만드는 권장 되지 않습니다.

보기 복잡 한 논리를 포함 하는 경우 논리 도우미 메서드를 이동 고려해 야 합니다. 웹 서버를 하지 않고 실행 하는 도우미 메서드에 대 한 단위 테스트를 작성할 수 있습니다.

> [!NOTE] 
> 
> 데이터 액세스 논리에 대해 테스트를 작성 또는 뷰 논리 좋은 방법이 아닙니다는 단위 테스트를 작성 하는 경우를 동안 건물 기능 또는 통합을 테스트 하는 경우 이러한 테스트 매우 유용할 수 있습니다.


> [!NOTE] 
> 
> ASP.NET MVC는 Web Forms 뷰 엔진입니다. Web Forms 뷰 엔진을 웹 서버에 종속 된 동안 다른 뷰 엔진 아닐 수 있습니다.


## <a name="using-a-mock-object-framework"></a>모의 개체 프레임 워크를 사용 하 여

단위 테스트를 작성할 때 거의 항상 모의 개체 프레임 워크를 활용 해야 합니다. 모의 개체 프레임 워크를 사용 하면 응용 프로그램에서 모의 개체 및 클래스에 대 한 스텁을 만들 수 있습니다.

예를 들어을 모의 버전의 저장소 클래스를 생성 하는 모의 개체 프레임 워크를 사용할 수 있습니다. 이런 방식으로 모의 리포지토리 클래스 단위 테스트에서 실제 저장소 클래스 대신 사용할 수 있습니다. 모의 리포지토리를 사용 하 여 단위 테스트를 실행 하는 경우 데이터베이스 코드를 실행 하지 않도록 수 있습니다.

Visual Studio의 모의 개체 프레임 워크를 포함 하지 않습니다. 그러나는 여러 개의 상용 및 오픈 소스 모의 개체 프레임 워크가.NET framework에 사용할 수 있는

1. Moq-이 프레임 워크는 오픈 소스 BSD 라이선스에 따라 사용할 수 있습니다. Moq에서 다운로드할 수 있습니다 [https://code.google.com/p/moq/](https://code.google.com/p/moq/)합니다.
2. Rhino Mocks-이 프레임 워크는 오픈 소스 BSD 라이선스 아래에 있습니다. Rhino Mocks에서 다운로드할 수 있습니다 [http://ayende.com/projects/rhino-mocks.aspx](http://ayende.com/projects/rhino-mocks.aspx)합니다.
3. Typemock 절연체-상용 프레임 워크입니다. 평가판 버전을 다운로드할 수 있습니다 [http://www.typemock.com/](http://www.typemock.com/)합니다.

이 자습서에서는 Moq 사용 하기로 합니다. 그러나 Rhino Mocks 손쉽게 사용할 수 있습니다 또는 모의 만들려는 Typemock 절연체 않아 응용 프로그램에 대 한 개체입니다.

Moq를 사용 하려면 먼저 다음 단계를 완료 해야 합니다.

1. 입니다.
2. 다운로드 압축을 푸는 전에 파일을 마우스 오른쪽 단추로 클릭 하 고 단추를 클릭 했는지 확인 **차단 해제** (그림 1 참조).
3. 다운로드를 압축을 풉니다.
4. ContactManager.Tests 프로젝트에서 References 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 Moq 어셈블리에 대 한 참조를 추가 **참조 추가**합니다. 찾아보기 탭에서 Moq의 압축을 푼 폴더를 찾아 Moq.dll 어셈블리를 선택 합니다. 클릭는 **확인** 단추입니다.
5. 다음이 단계를 완료 한 후 참조 폴더 그림 2와 같아야 합니다.


[![차단 해제 Moq](iteration-5-create-unit-tests-cs/_static/image1.jpg)](iteration-5-create-unit-tests-cs/_static/image1.png)

**그림 01**: 차단 해제 Moq ([전체 크기 이미지를 보려면 클릭](iteration-5-create-unit-tests-cs/_static/image2.png))


[![Moq를 추가한 후 참조](iteration-5-create-unit-tests-cs/_static/image2.jpg)](iteration-5-create-unit-tests-cs/_static/image3.png)

**그림 02**: Moq를 추가한 후 참조 ([전체 크기 이미지를 보려면 클릭](iteration-5-create-unit-tests-cs/_static/image4.png))


## <a name="creating-unit-tests-for-the-service-layer"></a>서비스 계층에 대 한 단위 테스트 만들기

우리의 않아 응용 프로그램의 서비스 계층에 대 한 단위 테스트의 집합을 만들어 시작 s를 사용 합니다. 이러한 테스트 유효성 검사 논리를 확인 하려면 사용 합니다.

ContactManager.Tests 프로젝트에서 모델을 라는 새 폴더를 만듭니다. 다음으로 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가, 새 테스트**합니다. **새 테스트 추가** 그림 3에 표시 된 대화 상자가 나타납니다. 선택은 **단위 테스트** 템플릿 ContactManagerServiceTest.cs 새 테스트 이름을 지정 합니다. 클릭는 **확인** 단추를 테스트 프로젝트에 새 테스트를 추가 합니다.

> [!NOTE] 
> 
> 일반적으로 ASP.NET MVC 프로젝트의 폴더 구조와 일치 하도록 테스트 프로젝트의 폴더 구조 지정 하려는 경우 예를 들어 컨트롤러 테스트 컨트롤러는 폴더에에서 배치, 모델 폴더에서 모델 테스트 및 등입니다.


[![Models\ContactManagerServiceTest.cs](iteration-5-create-unit-tests-cs/_static/image3.jpg)](iteration-5-create-unit-tests-cs/_static/image5.png)

**그림 03**: Models\ContactManagerServiceTest.cs ([전체 크기 이미지를 보려면 클릭](iteration-5-create-unit-tests-cs/_static/image6.png))


처음에 ContactManagerService 클래스에 의해 노출 CreateContact() 메서드를 테스트 하려고 합니다. 다음 다섯 가지 테스트를 만들겠습니다.

- CreateContact()-유효한 연락처 메서드에 전달 되 면 해당 CreateContact() 테스트 값 true를 반환 합니다.
- CreateContactRequiredFirstName()-경우에 누락 된 이름을 사용한 연락처 모델 상태 오류 메시지가 추가 되어 있는지 테스트 CreateContact() 메서드에 전달 됩니다.
- CreateContactRequredLastName()-테스트 오류 메시지가 모델 상태 때 누락 된 성 가진 연락처에 추가 됩니다 CreateContact() 메서드에 전달 됩니다.
- CreateContactInvalidPhone()-오류 메시지가 모델 상태 때 잘못 된 전화 번호에 대 한 연결이 추가 되어 있는지 테스트 CreateContact() 메서드에 전달 됩니다.
- CreateContactInvalidEmail()-테스트 오류 메시지가 모델 상태 때 잘못 된 전자 메일 주소를 가진 연락처에 추가 됩니다 CreateContact() 메서드에 전달 됩니다.

첫 번째 테스트 유효한 연락처 유효성 검사 오류를 생성 하지 않습니다 확인 합니다. 나머지 테스트 각 유효성 검사 규칙을 검사합니다.

이러한 테스트에 대 한 코드 목록 1에 포함 됩니다.

**1-Models\ContactManagerServiceTest.cs 나열**

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample1.cs)]


연락처 클래스 목록 1을 사용 하므로 테스트 프로젝트에 Microsoft Entity Framework에 대 한 참조를 추가 해야 합니다. System.Data.Entity 어셈블리에 대 한 참조를 추가 합니다.


목록 1 [TestInitialize] 특성으로 데코레이팅되는 initialize () 라는 메서드를 포함 합니다. 이 메서드는 자동으로 각 단위 테스트를 실행 하기 전에 (5 번 호출할 각 단위 테스트의 바로 앞). Initialize () 메서드는 코드의 다음 행으로 모의 리포지토리를 만듭니다.

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample2.cs)]

이 줄의 코드 Moq 프레임 워크를 사용 하 여 IContactManagerRepository 인터페이스에서 모의 리포지토리를 생성 합니다. 모의 리포지토리 각 단위 테스트를 실행할 때 데이터베이스에 액세스를 방지 하기 위해 실제 EntityContactManagerRepository 대신 사용 됩니다. 모의 리포지토리 IContactManagerRepository 인터페이스의 메서드를 구현 하지만 메서드 don t에 아무 것도 항목을 실제로 않습니다.

> [!NOTE] 
> 
> 사이는 차이가 없을 Moq 프레임 워크를 사용할 때 \_mockRepository 및 \_mockRepository.Object 합니다. 전자는 모의 가리킵니다&lt;IContactManagerRepository&gt; 모의 리포지토리 동작 하는 방법을 지정 하기 위한 메서드가 포함 된 클래스입니다. 참조 IContactManagerRepository 인터페이스를 구현 하는 실제 모의 리포지토리를 나타냅니다.


ContactManagerService 클래스의 인스턴스를 만들 때 모의 리포지토리 initialize () 메서드에서 사용 됩니다. 개별 단위 테스트의 모든 ContactManagerService 클래스의이 인스턴스를 사용합니다.

목록 1 각 단위 테스트에 해당 하는 다섯 가지 메서드가 포함 되어 있습니다. 이러한 각 방법의 [TestMethod] 특성으로 데코레이팅되 어 있습니다. 단위 테스트를 실행할 때이 특성을 가진 모든 메서드 호출 됩니다. 즉, [TestMethod] 특성으로 데코레이팅되는 모든 메서드는 단위 테스트 합니다.

CreateContact(), 명명 된 첫 번째 단위 테스트는 연락처 클래스의 올바른 인스턴스가 메서드에 전달 될 때 값이 true를 반환 CreateContact() 호출을 확인 합니다. 테스트는 연락처 클래스의 인스턴스를 만들고, CreateContact() 메서드를 호출 및 CreateContact() 값 true를 반환 하는지 확인 합니다.

나머지 테스트 확인 잘못 된 연락처와 CreateContact() 메서드를 호출할 때 다음 메서드에서 false가 반환 한 예상된 유효성 검사 오류 메시지가 모델 상태에 추가 됩니다. 예를 들어 CreateContactRequiredFirstName() 테스트 FirstName 속성에 대해 빈 문자열이 있는 연락처 클래스의 인스턴스를 만듭니다. 다음으로, 잘못 된 연락처와 CreateContact() 메서드가 호출 됩니다. 이 테스트 CreateContact() false를 반환 하 고 모델 상태 예상된 유효성 검사 오류 메시지를 "첫 번째 이름이 필요 합니다." 포함 되어 있는지 확인 하는 마지막으로,

메뉴 옵션을 선택 하 여 목록 1의 단위 테스트를 실행할 수 있습니다 **솔루션 (CTRL + R, A)의 모든 테스트를 실행할 테스트**합니다. 테스트의 결과 테스트 결과 창에 표시 됩니다 (그림 4 참조).


[![테스트 결과](iteration-5-create-unit-tests-cs/_static/image4.jpg)](iteration-5-create-unit-tests-cs/_static/image7.png)

**그림 04**: 테스트 결과 ([전체 크기 이미지를 보려면 클릭](iteration-5-create-unit-tests-cs/_static/image8.png))


## <a name="creating-unit-tests-for-controllers"></a>컨트롤러에 대 한 단위 테스트 만들기

ASP.NETMVC 응용 프로그램의 사용자 상호 작용 흐름을 제어 합니다. 컨트롤러를 테스트할 때는 컨트롤러 오른쪽 작업 결과 및 뷰 데이터를 반환 하는지 여부를 테스트 하려고 합니다. 컨트롤러를 예상 하는 방식에서 모델 클래스와 상호 작용 하는지 여부를 테스트 하려고 할 수 있습니다.

예를 들어 목록 2 연락처 컨트롤러 create () 메서드에 대 한 두 개의 단위 테스트를 포함합니다. 인덱스 작업에는 create () 메서드 리디렉션됩니다 유효한 연락처 create () 메서드에 전달 되 면 첫 번째 단위 테스트는 있는지 확인 합니다. 즉, 유효한 연락처를 전달 되는 경우 create () 메서드는 인덱스 작업을 나타내는 RedirectToRouteResult 반환 해야 합니다.

म 컨트롤러 레이어를 테스트 한다고 ContactManager 서비스 계층을 테스트 하는 원하지를 않는 합니다. 따라서 서비스 계층에서 Initialize 메서드를 다음 코드로 모의 했습니다.

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample3.cs)]

CreateValidContact() 단위 테스트에서 서비스 계층을 코드의 다음 줄 CreateContact() 메서드 호출의 동작에서는 모의 알림:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample4.cs)]

이 줄의 코드 하면 모의 ContactManager 서비스가 해당 CreateContact() 메서드를 호출할 때 값이 true를 반환 합니다. 서비스 계층, 모의에서는 컨트롤러의 동작을 서비스 계층의 모든 코드를 실행할 필요 없이 테스트할 수 있습니다.

두 번째 단위 테스트 확인 create () 동작 메서드에 잘못 된 대화 전달 되 면 만들기 뷰를 반환 합니다. म 발생 서비스 계층 CreateContact() 메서드 코드의 다음 행으로 값 false를 반환 합니다.

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample5.cs)]

Create () 메서드 의도 한 대로 동작 하는 경우 서비스 계층 값 false를 반환 하는 경우 만들기 뷰를 반환 해야 합니다. 이런 방식으로 컨트롤러 만들기 뷰에 유효성 검사 오류 메시지를 표시할 수 있으며 사용자는 잘못 된 연락처 속성을 수정할 수 있는 기회입니다.


컨트롤러에 대 한 단위 테스트를 빌드 하려는 경우 컨트롤러 작업에서 명시적 보기 이름을 반환 해야 합니다. 예를 들어 다음과 같은 보기를 반환 하지 않습니다.

View(); 반환

대신, 다음과 같은 보기를 반환할 수 있습니다.

View("Create"); 반환

없는 경우 명시적 보기를 반환할 때 ViewResult.ViewName 속성은 빈 문자열을 반환 합니다.


**2-Controllers\ContactControllerTest.cs 나열**

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample6.cs)]

## <a name="summary"></a>요약

이 반복에 않아 응용 프로그램에 대 한 단위 테스트 생성 합니다. 언제 든 지 응용 프로그램 라고 생각 하는 방식으로 계속 동작을 확인 하려면 이러한 단위 테스트를 실행할 수 있습니다. 단위 테스트는 나중에 응용 프로그램을 안전 하 게 수정할 수 있어 응용 프로그램에 대 한 안전망 역할.

두 개의 단위 테스트 집합이 만들었는지 여부입니다. 첫째, 유효성 검사 논리는 서비스 계층에 대 한 단위 테스트를 만들어 테스트 했습니다. 다음으로,이 흐름 제어 논리 우리의 컨트롤러 계층에 대 한 단위 테스트를 만들어 테스트 합니다. 이 서비스 계층을 테스트할 때 म 별로 격리 된 테스트 우리의 서비스 계층에 대 한 우리의 저장소 계층에서 모의 리포지토리 계층 우리의 합니다. 컨트롤러 계층을 테스트할 때 म 별로 격리 된 테스트 우리의 컨트롤러 계층에 대 한 서비스 계층 모의 합니다.

다음 반복에서 우리 않아 응용 프로그램 되도록 수정 메일 그룹을 지원 합니다. 이 새로운 기능 테스트 기반 개발 소프트웨어 디자인 프로세스를 사용 하 여 응용 프로그램에 추가 합니다.

>[!div class="step-by-step"]
[이전](iteration-4-make-the-application-loosely-coupled-cs.md)
[다음](iteration-6-use-test-driven-development-cs.md)
