---
uid: mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
title: '반복 #4 – 확인 응용 프로그램을 느슨하게 결합 (C#) | Microsoft Docs'
author: microsoft
description: 이 세 번째 반복에서는 활용 쉽게 유지 관리 하 고 연락처 관리자 응용 프로그램을 수정 하려면 몇 가지 소프트웨어 디자인 패턴입니다. For...
ms.author: aspnetcontent
ms.date: 02/20/2009
ms.assetid: 829f589f-e201-4f6e-9ae6-08ae84322065
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
msc.type: authoredcontent
ms.openlocfilehash: 8eff8088398d0f7afc020b2bbdf41526ae51591a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37829501"
---
<a name="iteration-4--make-the-application-loosely-coupled-c"></a>반복 #4 – 응용 프로그램을 느슨하게 결합 (C#) 확인
====================
[Microsoft](https://github.com/microsoft)

[코드 다운로드](iteration-4-make-the-application-loosely-coupled-cs/_static/contactmanager_4_cs1.zip)

> 이 세 번째 반복에서는 활용 쉽게 유지 관리 하 고 연락처 관리자 응용 프로그램을 수정 하려면 몇 가지 소프트웨어 디자인 패턴입니다. 예를 들어, 리포지토리 패턴 및 종속성 주입 패턴을 사용 하 여 응용 프로그램을 리팩터링 했습니다.


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

연락처 관리자 응용 프로그램의이 네 번째 반복에서 응용 프로그램 더 느슨하게 결합 된 응용 프로그램을 리팩터링 했습니다. 응용 프로그램은 느슨하게 결합 되어 있는 경우에 응용 프로그램의 다른 부분에서 코드를 수정 하지 않고도 응용 프로그램의 한 부분에서 코드를 수정할 수 있습니다. 느슨하게 결합 된 응용 프로그램은 변경 복원 력을 높입니다.

현재 모든 연락처 관리자 응용 프로그램에서 사용 되는 데이터 액세스 및 유효성 검사 논리는 컨트롤러 클래스에 포함 됩니다. 이 않는 것이 좋습니다. 응용 프로그램의 한 부분을 수정 해야 할 경우 응용 프로그램의 다른 부분에 버그가 발생할 수 있습니다. 예를 들어 사용자 유효성 검사 논리를 수정 하면 위험이 있습니다 데이터 액세스 또는 컨트롤러 논리에 대 한 새 버그가 있습니다.

> [!NOTE] 
> 
> (SRP) 클래스는 둘 이상의 변경할 이유가 없습니다. 대규모 단일 책임 원칙을 위반 하는 컨트롤러, 유효성 검사 및 데이터베이스 논리를 혼합 합니다.


응용 프로그램을 수정 해야 할 수 있는 방법은 여러 가지가 있습니다. 응용 프로그램에 새 기능을 추가 해야 하 고, 응용 프로그램에서 버그를 수정 해야 할 수 있습니다 또는 응용 프로그램의 기능 구현 되는 방식을 수정 해야 할 수 있습니다. 응용 프로그램은 정적 거의 없습니다. 경향이 증가 하 고 시간이 지남에 따라 변경 합니다.

예를 들어, 데이터 액세스 계층을 구현 하는 방법을 변경 하려는 한다고 가정 합니다. 오른쪽 이제 연락처 관리자 응용 프로그램 Microsoft Entity Framework를 사용 데이터베이스에 액세스할 수 있습니다. 그러나 ADO.NET Data Services 또는 NHibernate 같은 새로운 또는 다른 데이터 액세스 기술으로 마이그레이션할 수도 있습니다. 그러나 데이터 액세스 코드를 유효성 검사 및 컨트롤러 코드에서 격리 없는 이므로 데이터 액세스 직접 관련이 없는 다른 코드를 수정 하지 않고 응용 프로그램에서 데이터 액세스 코드를 수정할 수 없습니다.

응용 프로그램은 느슨하게 결합 되어 있는 경우 다른 한편으로 할 수 있습니다 변경 내용을 응용 프로그램의 한 부분에는 응용 프로그램의 다른 부분을 건드리지 않고. 예를 들어, 컨트롤러 또는 유효성 검사 논리를 수정 하지 않고 데이터 액세스 기술을 전환할 수 있습니다.

이 반복에서 점을 이용 더 느슨하게 결합 된 응용 프로그램으로 연락처 관리자 응용 프로그램을 리팩터링 하는 몇 가지 소프트웨어 디자인 패턴입니다. 작업을 완료 했습니다 t-이득 Contact Manager 수행할는 해당 동작 t 전에 작업을 수행 합니다. 그러나 나중에 보다 쉽게 응용 프로그램을 변경 하려면 드리겠습니다.

> [!NOTE] 
> 
> 리팩터링 하는 것은 기존 기능이 손실 되지 않습니다 하는 방식으로 응용 프로그램을 다시 작성 하는 프로세스입니다.


## <a name="using-the-repository-software-design-pattern"></a>리포지토리 소프트웨어 디자인 패턴을 사용 하 여

첫 번째 변경 리포지토리 패턴을 호출 하는 소프트웨어 디자인 패턴을 활용 하는 것입니다. 응용 프로그램의 나머지 부분에서 데이터 액세스 코드를 격리 하는 리포지토리 패턴을 사용 하겠습니다.

리포지토리 패턴을 구현 하려면 다음 두 단계를 완료 하기:

1. 인터페이스 만들기
2. 인터페이스를 구현 하는 구체적인 클래스 만들기

먼저 모든 수행 해야 하는 데이터 액세스 메서드를 설명 하는 인터페이스를 만드는 해야 합니다. IContactManagerRepository 인터페이스 목록 1에 포함 됩니다. 이 인터페이스는 5 개의 메서드를 설명 합니다: CreateContact() "," DeleteContact() "," EditContact() "," GetContact, "및" ListContacts() 합니다.

**1-Models\IContactManagerRepositiory.cs 나열**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample1.cs)]

다음으로, IContactManagerRepository 인터페이스를 구현 하는 구체적인 클래스를 만드는 해야 합니다. Microsoft Entity Framework 데이터베이스 액세스를 사용 하기 때문에 EntityContactManagerRepository 라는 새 클래스를 만들겠습니다. 이 클래스는 목록 2에 포함 됩니다.

**Listing 2 - Models\EntityContactManagerRepository.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample2.cs)]

EntityContactManagerRepository 클래스 IContactManagerRepository 인터페이스를 구현 하는지 확인 합니다. 클래스에는 5 개 모두에서 해당 인터페이스에서 설명 하는 방법의 구현 합니다.

인터페이스를 사용 해야 하는 이유가 궁금할 것입니다. 인터페이스와 구현 하는 클래스를 만드는 이유는 필요한 무엇입니까?

단, 응용 프로그램의 나머지 부분에서는 구체적인 클래스가 아니라 인터페이스와 상호 작용 합니다. EntityContactManagerRepository 클래스에 의해 노출 되는 메서드를 호출 하지 않고 IContactManagerRepository 인터페이스에 의해 노출 되는 메서드 호출 합니다.

이런 방식으로 응용 프로그램의 나머지 부분을 수정 하지 않고도 새 클래스를 사용 하 여 인터페이스를 구현할 수 있습니다. 예를 들어, 일부 미래 날짜에 것이 좋습니다 IContactManagerRepository 인터페이스를 구현 하는 DataServicesContactManagerRepository 클래스를 구현 하려면. DataServicesContactManagerRepository 클래스는 Microsoft Entity Framework는 대신 데이터베이스에 액세스 하려면 ADO.NET Data Services를 사용할 수 있습니다.

응용 프로그램 코드 구체적인 EntityContactManagerRepository 클래스 대신 IContactManagerRepository 인터페이스에 대해 프로그래밍 하는 경우 코드의 나머지 부분 중 하나를 수정 하지 않고 구체적 클래스를 전환할 수 했습니다. 예를 들어,이 데이터 액세스 또는 유효성 검사 논리를 수정 하지 않고 DataServicesContactManagerRepository 클래스 EntityContactManagerRepository 클래스에서 전환할 수 했습니다.

구체적인 클래스가 아닌 인터페이스 (추상화)에 대 한 프로그래밍을 사용 하면 응용 프로그램 변경 복원 력을 높입니다.

> [!NOTE] 
> 
> 메뉴 옵션을 리팩터링, 인터페이스 추출를 선택 하 여 Visual Studio 내에서 구체적 클래스에서 인터페이스를 신속 하 게 만들 수 있습니다. 예를 들어 EntityContactManagerRepository 클래스를 먼저 만든 하 수를 사용 하 여 인터페이스 추출 IContactManagerRepository 인터페이스를 자동으로 생성 합니다.


## <a name="using-the-dependency-injection-software-design-pattern"></a>종속성 주입 소프트웨어 디자인 패턴을 사용 하 여

데이터 액세스 코드를 별도 리포지토리 클래스를 마이그레이션에서는이 클래스를 사용 하 여 연락처 컨트롤러를 수정 해야 합니다. 에서는 컨트롤러에서 리포지토리 클래스를 사용 하는 종속성 주입을 호출 하는 소프트웨어 디자인 패턴의 이점은 걸립니다.

수정 된 연락처 컨트롤러 목록 3에 포함 됩니다.

**3-Controllers\ContactController.cs 나열**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample3.cs)]

목록 3에서 연락처 컨트롤러에 두 명의 생성자가 있는지 확인 합니다. 첫 번째 생성자는 두 번째 생성자는 IContactManagerRepository 인터페이스의 구체적인 인스턴스를 전달합니다. 연락처 컨트롤러 클래스 사용 *생성자 종속성 주입*합니다.

및 EntityContactManagerRepository 클래스는 현재 위치에만 첫 번째 생성자는입니다. 클래스의 나머지 부분에서는 구체적인 EntityContactManagerRepository 클래스 대신 IContactManagerRepository 인터페이스를 사용합니다.

따라서 쉽게 IContactManagerRepository 클래스의 구현은 앞으로 전환할 수 있습니다. EntityContactManagerRepository 클래스 대신 DataServicesContactRepository 클래스를 사용 하려는 경우 첫 번째 생성자는 수정 합니다.

생성자 종속성 주입을 높입니다 연락처 컨트롤러 클래스를 매우 테스트할 수 있습니다. 단위 테스트를 IContactManagerRepository 클래스의 모의 구현을 전달 하 여 연락처 컨트롤러를 인스턴스화할 수 있습니다. 이 기능의 종속성 주입에서는 연락처 관리자 응용 프로그램에 대 한 단위 테스트를 작성 하는 경우 다음 반복에서 우리에 게 매우 중요 한 됩니다.

> [!NOTE] 
> 
> 완전히 IContactManagerRepository 인터페이스의 특정 구현에서 연락처 컨트롤러 클래스를 분리 하려는 경우 다음 있습니다 활용 StructureMap 등 Microsoft 종속성 주입을 지 원하는 프레임 워크 Entity Framework (MEF)입니다. 종속성 주입 프레임 워크를 활용 하 여 코드에서 구체적 클래스를 참조할 필요가 없습니다.


## <a name="creating-a-service-layer"></a>서비스 레이어 만들기

보시는 유효성 검사 논리는 여전히 혼합 목록 3의 수정 된 컨트롤러 클래스에서이 컨트롤러 논리를 사용 하 여 합니다. 이 데이터 액세스 논리를 격리 하는 것이 좋습니다는 마찬가지 이유로, 것이 유효성 검사 논리를 격리 하는 것이 좋습니다.

이 문제를 해결 하려면 별도 만들 수 있습니다 [ *서비스 계층*](http://martinfowler.com/eaaCatalog/serviceLayer.html)합니다. 서비스 계층은 리포지토리 클래스는 컨트롤러 사이의 삽입 수는 별도 계층입니다. 서비스 계층에 모든 유효성 검사 논리를 포함 하는 비즈니스 논리를 포함 합니다.

ContactManagerService 4에 포함 됩니다. 연락처 컨트롤러 클래스의 유효성 검사 논리를 포함합니다.

**4-Models\ContactManagerService.cs 나열**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample4.cs)]

ContactManagerService 생성자는 ValidationDictionary 해야 한다는 것을 확인 합니다. 서비스 계층을 통해이 ValidationDictionary 컨트롤러 계층 통신할 수 있습니다. Decorator 패턴을 설명할 때 다음 섹션에서 자세히 ValidationDictionary 설명 합니다.

표시, 또한를 ContactManagerService IContactManagerService 인터페이스를 구현 하는 합니다. 항상 구체적인 클래스가 아닌 인터페이스를 프로그래밍할 하도록 해야 합니다. 연락처 관리자 응용 프로그램의 다른 클래스 직접 ContactManagerService 클래스 상호 작용 하지 않습니다. 대신 한 가지 예외로 연락처 관리자 응용 프로그램의 나머지 부분에 대해 프로그래밍 IContactManagerService 인터페이스.

IContactManagerService 인터페이스 목록 5에 포함 됩니다.

**5-Models\IContactManagerService.cs 나열**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample5.cs)]

수정 된 연락처 컨트롤러 클래스 목록 6에 포함 됩니다. 연락처 컨트롤러 ContactManager 리포지토리를 사용 하 여 더 이상 상호 작용 한다고 확인 합니다. 대신, 연락처 컨트롤러 ContactManager 서비스와 상호 작용 합니다. 각 계층은 다른 계층에서 최대한 격리 됩니다.

**6-Controllers\ContactController.cs 나열**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample6.cs)]

더 이상 응용 프로그램에 단일 책임 원칙 (SRP)을 위반 실행 합니다. 응용 프로그램 실행의 흐름 제어 이외의 모든 책임 연락처 컨트롤러 목록 6에서 제거 되었습니다. 모든 유효성 검사 논리가 연락처 컨트롤러에서 제거 되었으며 서비스 계층에 푸시됩니다. 모든 데이터베이스 논리 저장소 계층으로 푸시 되었습니다.

## <a name="using-the-decorator-pattern"></a>데코레이터 패턴을 사용 하 여

이 컨트롤러 계층에서이 서비스 계층을 완전히 분리 수 있으려면 하고자 합니다. 원칙적으로 돌아가 MVC 응용 프로그램에 대 한 참조를 추가할 필요 없이 컨트롤러 계층에서 별도 어셈블리에는 서비스 계층을 컴파일할 수 있어야 합니다.

그러나이 서비스 계층 컨트롤러 계층에 다시 유효성 검사 오류 메시지를 전달할 수 해야 합니다. 컨트롤러 및 서비스 계층을 결합 하지 않고 유효성 검사 오류 메시지를 통신 하도록 서비스 계층에는 어떻게 설정할 수 있습니다.에서는? 라는 소프트웨어 디자인 패턴을 활용 합니다 [데코레이터 패턴](http://en.wikipedia.org/wiki/Decorator_pattern)합니다.

컨트롤러는 ModelStateDictionary ModelState 라는 사용 하 여 유효성 검사 오류를 나타냅니다. 따라서 ModelState 컨트롤러 계층에서 서비스 계층에 전달 하 고 싶은 생각이 들 수 있습니다. 그러나 ModelState를 사용 하 여 서비스 계층에는 서비스 계층에 종속 되 게 ASP.NET MVC 프레임 워크의 기능입니다. ASP.NET MVC 응용 프로그램 대신 WPF 응용 프로그램을 사용 하 여 서비스 계층을 사용 하려는 향후 때문에 잘못 된 것. 이 경우 비현실적 t ModelStateDictionary 클래스를 사용 하 여 ASP.NET MVC 프레임 워크를 참조 하려고 합니다.

Decorator 패턴을 사용 하는 인터페이스를 구현 하기 위해 새 클래스에서 기존 클래스를 래핑할 수 있습니다. Contact Manager 프로젝트는 7에 포함 된 ModelStateWrapper 클래스를 포함 합니다. ModelStateWrapper 클래스 목록 8에서 인터페이스를 구현합니다.

**Listing 7 - Models\Validation\ModelStateWrapper.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample7.cs)]

**8-Models\Validation\IValidationDictionary.cs 나열**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample8.cs)]

목록 5의 세부적인 모습을 사용 하는 경우 표시 됩니다 ContactManager 서비스 계층 IValidationDictionary 인터페이스를 단독으로 사용 합니다. ContactManager 서비스 ModelStateDictionary 클래스에 종속 되지 않습니다. 연락처 컨트롤러 ContactManager 서비스를 만들 때 컨트롤러 다음과 같이 해당 ModelState를 래핑합니다.

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample9.cs)]

## <a name="summary"></a>요약

이 반복에서 연락처 관리자 응용 프로그램에 새로운 기능을 추가 하지 않았습니다. 이 반복의 목적은 유지 관리 하 고 수정 하기가 정말 연락처 관리자 응용 프로그램을 리팩터링 하는 것 이었습니다.

첫째, 리포지토리 소프트웨어 디자인 패턴을 구현 했습니다. 데이터 액세스 코드를 모두 마이그레이션할 별도 ContactManager 리포지토리 클래스입니다.

에서는 컨트롤러 논리에서 유효성 검사 논리를 분리 됩니다. 모든 유효성 검사 코드를 포함 하는 별도 서비스 계층을 만들었습니다. 서비스 계층을 사용 하 여 컨트롤러 계층 상호 작용 하 고 서비스 계층은 리포지토리 계층 상호 작용 합니다.

서비스 계층을 만들 때이 서비스 계층에서 ModelState 격리 Decorator 패턴의 장점은 했습니다. 이 서비스 계층에서 ModelState 대신 IValidationDictionary 인터페이스에 대 한 프로그래밍 합니다.

마지막으로, 종속성 주입 패턴 이라는 소프트웨어 디자인 패턴을 활용을 했습니다. 이 패턴 (추상화) 구체적인 클래스가 아닌 인터페이스를 프로그래밍할 수 있습니다. 종속성 주입 디자인 패턴을 구현할 뿐만 아니라 코드 보다 테스트 됩니다. 다음 반복에서 단위 테스트 프로젝트를 추가할 것입니다.

> [!div class="step-by-step"]
> [이전](iteration-3-add-form-validation-cs.md)
> [다음](iteration-5-create-unit-tests-cs.md)
