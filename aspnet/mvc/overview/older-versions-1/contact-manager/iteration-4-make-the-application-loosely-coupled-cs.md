---
uid: mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
title: '반복 #4 – 느슨하게 결합 된 응용 프로그램 (C#)으로 설정 | Microsoft Docs'
author: microsoft
description: 이 세 번째 반복에서 우리 활용 여러 가지 소프트웨어 디자인 패턴을 쉽게 유지 관리 하 고 않아 응용 프로그램을 수정 합니다. For...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: 829f589f-e201-4f6e-9ae6-08ae84322065
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
msc.type: authoredcontent
ms.openlocfilehash: 33221c6c3326c7034fe013f152579828e2fc8a3a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="iteration-4--make-the-application-loosely-coupled-c"></a>반복 #4 – 느슨하게 결합 된 응용 프로그램 (C#)으로 설정
====================
by [Microsoft](https://github.com/microsoft)

[코드 다운로드](iteration-4-make-the-application-loosely-coupled-cs/_static/contactmanager_4_cs1.zip)

> 이 세 번째 반복에서 우리 활용 여러 가지 소프트웨어 디자인 패턴을 쉽게 유지 관리 하 고 않아 응용 프로그램을 수정 합니다. 예를 들어 리팩터링한 리포지토리 패턴 및 종속성 주입 패턴을 사용 하도록 응용 프로그램입니다.


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

않아 응용 프로그램의 네 번째 반복이 더 느슨하게 결합 된 응용 프로그램을 응용 프로그램을 리팩터링한 합니다. 응용 프로그램은 느슨하게 결합 되어 있는 경우에 응용 프로그램의 다른 부분에 코드를 수정 하지 않고도 응용 프로그램의 한 부분에 있는 코드를 수정할 수 있습니다. 느슨하게 결합 된 응용 프로그램을 변경 하려면 복원 성도 뛰어납니다.

현재 모든 연락처 관리자 응용 프로그램에서 사용 하는 데이터 액세스 및 유효성 검사 논리는 컨트롤러 클래스에 포함 됩니다. 이 않는 것이 좋습니다. 응용 프로그램의 한 부분을 수정 해야 할 때마다 응용 프로그램의 다른 부분에 버그를 도입할 발생할 수 있습니다. 예를 들어 유효성 검사 논리를 수정 하는 경우 위험이 있습니다 데이터 액세스 또는 컨트롤러 논리에 새로운 버그를 도입 합니다.

> [!NOTE] 
> 
> (SRP) 클래스는 둘 이상의 변경할 이유가 필요는 합니다. 컨트롤러, 유효성 검사 및 데이터베이스 논리를 혼합 하는 것은 대규모 위반 단일 책임 원칙입니다.


응용 프로그램을 수정 해야 할 수 있는 방법은 여러 가지가 있습니다. 응용 프로그램에 새로운 기능을 추가 해야 할 수, 응용 프로그램에서 버그를 수정 해야 할 수 있습니다 또는 응용 프로그램의 기능을 구현 하는 방법을 수정 해야 할 수 있습니다. 응용 프로그램은 정적 거의 없습니다. 경향이 증가 하 고 시간이 지남에 따라 변경 합니다.

예를 들어, 데이터 액세스 계층을 구현 하는 방법을 변경 하려는 한다고 가정 합니다. 오른쪽 이제 않아 응용 프로그램을 사용 하 여 Microsoft Entity Framework 데이터베이스에 액세스 합니다. ADO.NET Data Services 또는 NHibernate 등 새로운 또는 다른 데이터 액세스 기술으로 마이그레이션할 수도 있습니다. 그러나 없기 때문에 데이터 액세스 코드 유효성 검사 및 컨트롤러 코드에서 격리 되지 않은, 데이터 액세스 직접 관련이 없는 다른 코드를 수정 하지 않고 응용 프로그램에서 데이터 액세스 코드를 수정할 수 없습니다.

응용 프로그램은 느슨하게 결합 되어 있는 경우 반면에 수 변경 하면 응용 프로그램의 한 부분에 응용 프로그램의 다른 부분을 터치 하지 않고도 됩니다. 예를 들어 컨트롤러 또는 유효성 검사 논리를 수정 하지 않고 데이터 액세스 기술을 전환할 수 있습니다.

이 반복에서 우리 활용 느슨하게 결합 된 응용 프로그램으로 않아 응용 프로그램을 리팩터링 하는 여러 가지 소프트웨어 디자인 패턴. 때는 작업을 완료 했습니다 t 성공한 않아 아무 작업도 수행 하는 것 않았음에도 t 전에 작업을 수행 합니다. 그러나 나중에 보다 쉽게 응용 프로그램을 변경할 수 있습니다.

> [!NOTE] 
> 
> 리팩터링은 기존 기능이 손실 되지 않는 방식으로 응용 프로그램을 다시 작성 하는 과정을 됩니다.


## <a name="using-the-repository-software-design-pattern"></a>리포지토리 소프트웨어 디자인 패턴을 사용 하 여

이 첫 번째 변경 사항을 리포지토리 패턴 이라는 소프트웨어 디자인 패턴을 활용 하는 것입니다. 응용 프로그램의 나머지 부분에서 데이터 액세스 코드를 격리 하려면 리포지토리 패턴을 사용 합니다.

리포지토리 패턴을 구현 하려면 다음 두 단계를 완료 하기:

1. 인터페이스를 만듭니다
2. 인터페이스를 구현 하는 구체적인 클래스 만들기

첫째, 모든 수행 해야 하 고 데이터 액세스 메서드를 설명 하는 인터페이스를 만드는 필요 합니다. IContactManagerRepository 인터페이스 목록 1에 포함 됩니다. 이 인터페이스는 5 개의 메서드를 설명: CreateContact(), DeleteContact(), EditContact(), GetContact, 및 ListContacts() 합니다.

**Listing 1 - Models\IContactManagerRepositiory.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample1.cs)]

다음으로, IContactManagerRepository 인터페이스를 구현 하는 구체적인 클래스를 만드는 필요 합니다. Microsoft Entity Framework 데이터베이스에 액세스, 사용 중 이므로 EntityContactManagerRepository 라는 새 클래스를 만들겠습니다. 이 클래스는 목록 2에 포함 됩니다.

**Listing 2 - Models\EntityContactManagerRepository.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample2.cs)]

EntityContactManagerRepository 클래스 IContactManagerRepository 인터페이스를 구현 하는지 확인 합니다. 5 해당 인터페이스에 설명 된 방법 모두 구현 하는 클래스입니다.

인터페이스를 필요한 이유가 궁금할 것입니다. 구현 하는 클래스와 인터페이스를 만드는 이유 필요한 무엇입니까?

단, 응용 프로그램의 나머지 부분에서는 구체적인 클래스가 아닌 인터페이스와 상호 작용 합니다. EntityContactManagerRepository 클래스에 의해 노출 되는 메서드를 호출 하는 대신 IContactManagerRepository 인터페이스에 의해 노출 되는 메서드 라고 합니다.

이런 방식으로 응용 프로그램의 나머지 부분을 수정 하지 않고도 새 클래스와 인터페이스를 구현할 수 있습니다. 예를 들어에 미래의 특정 날짜, IContactManagerRepository 인터페이스를 구현 하는 DataServicesContactManagerRepository 클래스를 구현 하려고 수 있습니다. DataServicesContactManagerRepository 클래스 Microsoft 엔터티 프레임 워크는 대신 데이터베이스에 액세스 하려면 ADO.NET Data Services를 사용할 수 있습니다.

응용 프로그램 코드 구체적인 EntityContactManagerRepository 클래스 대신 IContactManagerRepository 인터페이스에 대해 프로그래밍 하는 경우 코드의 나머지 부분을 수정 하지 않고 구체적 클래스를 전환할 수 있습니다. 예를 들어 전환할 수 있습니다 EntityContactManagerRepository 클래스에서 DataServicesContactManagerRepository 클래스에이 데이터 액세스 또는 유효성 검사 논리를 수정 하지 않고 있습니다.

구체적인 클래스가 아닌 인터페이스 (추상화)에 대 한 프로그래밍을 사용 하면 응용 프로그램을 변경 하려면 복원 성도 뛰어납니다.

> [!NOTE] 
> 
> 인터페이스 추출 메뉴 옵션 리팩터링을 선택 하 여 Visual Studio 내에서 구체적인 클래스에서 인터페이스를 빠르게 만들 수 있습니다. 예를 들어 있습니다 수 EntityContactManagerRepository 클래스 먼저 만들고 사용 하 여 인터페이스 추출 IContactManagerRepository 인터페이스를 자동으로 생성할 수 있습니다.


## <a name="using-the-dependency-injection-software-design-pattern"></a>종속성 주입 소프트웨어 디자인 패턴을 사용 하 여

데이터 액세스 코드 마이그레이션한 우리는 별도 저장소 클래스를 했으므로이 클래스를 사용 하 여 연락처 컨트롤러를 수정 해야 합니다. 컨트롤러에서 저장소 클래스를 사용 하는 종속성 주입을 호출 하는 소프트웨어 디자인 패턴의 장점은 해당 메뉴로 이동 합니다.

수정 된 연락처 컨트롤러 목록 3에 포함 됩니다.

**3-Controllers\ContactController.cs 나열**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample3.cs)]

연락처 컨트롤러 목록 3에 두 명의 생성자가 있는지 확인 합니다. 첫 번째 생성자는 두 번째 생성자는 IContactManagerRepository 인터페이스의 구체적인 인스턴스로 전달합니다. 연락처 컨트롤러 클래스 사용 하 여 *생성자 종속성 주입*합니다.

첫 번째 생성자는 한, EntityContactManagerRepository 클래스 사용 되는 장소만입니다. 클래스의 나머지 부분에서는 구체적인 EntityContactManagerRepository 클래스 대신 IContactManagerRepository 인터페이스를 사용합니다.

따라서 쉽게 IContactManagerRepository 클래스의 구현 앞으로 전환할 수 있습니다. EntityContactManagerRepository 클래스 대신 DataServicesContactRepository 클래스를 사용 하려는 경우 첫 번째 생성자는 수정 합니다.

생성자 종속성 주입을 사용 하면 연락처 컨트롤러 클래스 매우 테스트할 수 있습니다. 단위 테스트를 모의 구현을 IContactManagerRepository 클래스를 전달 하 여 연락처 컨트롤러를 인스턴스화할 수 있습니다. 우리가 않아 응용 프로그램에 대 한 단위 테스트를 구축 하는 경우이 기능 종속성 주입을 매우 소중 하 게 다룹니다 다음 반복에 됩니다.

> [!NOTE] 
> 
> 완전히 IContactManagerRepository 인터페이스의 특정 구현에서 연락처 컨트롤러 클래스를 분리 하려면 다음 있습니다 활용할 수 StructureMap 또는 Microsoft와 같은 종속성 주입을 지원 되는 프레임 워크 Entity Framework (MEF)입니다. 종속성 주입 프레임 워크를 활용 하면 코드의 구체적인 클래스를 참조할 필요가 없습니다.


## <a name="creating-a-service-layer"></a>서비스 계층을 만들려면

알 수 있습니다는 컨트롤러 논리 목록 3에서 수정 된 컨트롤러 클래스에 유효성 검사 논리 혼합 여전히 됩니다. 이 데이터 액세스 논리를 격리 하는 것이 좋습니다 임을 개발한 것이 좋습니다는 유효성 검사 논리를 격리 하 합니다.

이 문제를 해결 하려면 별도 만들면 [ *서비스 계층*](http://martinfowler.com/eaaCatalog/serviceLayer.html)합니다. 서비스 계층은 우리의 컨트롤러 및 리포지토리 클래스 사이 삽입할 수 있습니다 하는 별도 계층입니다. 서비스 계층에는 모든 유효성 검사 논리를 포함 하 여이 비즈니스 논리를 포함 합니다.

ContactManagerService 목록 4에 포함 되어 있습니다. 연락처 컨트롤러 클래스에서 유효성 검사 논리를 포함 합니다.

**Listing 4 - Models\ContactManagerService.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample4.cs)]

ContactManagerService에 대 한 생성자는 ValidationDictionary 해야 한다는 것을 확인 합니다. 서비스 계층이이 ValidationDictionary 통해 컨트롤러 계층과 통신 합니다. Decorator 패턴을 설명할 때 ValidationDictionary 다음 섹션에서 자세히 설명 합니다.

또한는 ContactManagerService IContactManagerService 인터페이스를 구현 하는지 확인할 수 있습니다. 항상 구체적인 클래스가 아닌 인터페이스에 대 한 프로그램 하도록 해야 합니다. 않아 응용 프로그램의 다른 클래스 직접 ContactManagerService 클래스 상호 작용 하지 않습니다. 대신, 한 가지 예외로 않아 응용 프로그램의 나머지 부분에 대해 프로그래밍 IContactManagerService 인터페이스.

IContactManagerService 인터페이스 목록 5에 포함 됩니다.

**Listing 5 - Models\IContactManagerService.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample5.cs)]

수정 된 연락처 컨트롤러 클래스 목록 6에 포함 됩니다. 연락처 컨트롤러가 ContactManager 리포지토리와 상호 작용 더 이상 확인 합니다. 대신, 연락처 컨트롤러 ContactManager 서비스와 상호 작용 합니다. 각 레이어는 다른 계층에서 가능한 한 격리 합니다.

**Listing 6 - Controllers\ContactController.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample6.cs)]

더 이상 응용 프로그램에 단일 책임 원칙 (SRP)의 위반을 실행 합니다. 응용 프로그램 실행 흐름 제어 이외의 모든 책임 연락처 컨트롤러 목록 6에서 제거 되었습니다. 모든 유효성 검사 논리 연락처 컨트롤러에서 제거 되었으며 서비스 계층에 푸시됩니다. 모든 데이터베이스 논리 저장소 계층에 밀어넣은 합니다.

## <a name="using-the-decorator-pattern"></a>Decorator 패턴을 사용 하 여

완전히 우리의 컨트롤러 계층에서이 서비스 계층을 분리할 수 있게 되기를 원하는 합니다. 원칙적으로 MVC 응용 프로그램에 대 한 참조를 사용 하지 않고 우리의 컨트롤러 계층에서 별도 어셈블리에서이 서비스 계층을 컴파일할 수 있습니다.

그러나이 서비스 계층을 컨트롤러 계층에 다시 유효성 검사 오류 메시지를 전달할 수 해야 합니다. 서비스 계층, 컨트롤러 및 서비스 계층을 결합 하지 않고 유효성 검사 오류 메시지를 통신 하도록 하려면 어떻게 해야 우리? 라는 소프트웨어 디자인 패턴의 이용할 수 있습니다는 [Decorator 패턴](http://en.wikipedia.org/wiki/Decorator_pattern)합니다.

컨트롤러는 ModelState 라는 ModelStateDictionary를 사용 하 여 유효성 검사 오류를 나타냅니다. 따라서 서비스 계층으로 컨트롤러 레이어에서 ModelState 전달 하려고 시도할 수 있습니다. 그러나 ModelState를 사용 하 여 서비스 계층에는 서비스 계층에 종속 되 게 ASP.NET MVC 프레임 워크의 기능입니다. 서비스 계층을 사용 하 여 WPF 응용 프로그램에서 ASP.NET MVC 응용 프로그램 대신 할 언젠가 때문에 잘못 된 것입니다. 이 경우 t 비현실적 ModelStateDictionary 클래스를 사용 하려면 ASP.NET MVC 프레임 워크 참조 하려고 합니다.

Decorator 패턴을 사용 하면 새 클래스에 인터페이스를 구현 하는 데 기존 클래스를 래핑할 수 있습니다. 우리의 않아 프로젝트 목록 7에 포함 된 ModelStateWrapper 클래스를 포함 합니다. ModelStateWrapper 클래스 목록 8에는 인터페이스를 구현합니다.

**Listing 7 - Models\Validation\ModelStateWrapper.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample7.cs)]

**Listing 8 - Models\Validation\IValidationDictionary.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample8.cs)]

목록 5를 자세히 검토를 사용 하는 경우 것을 확인할 수 ContactManager 서비스 계층 IValidationDictionary 인터페이스를 단독으로 사용 합니다. ContactManager 서비스 ModelStateDictionary 클래스에 종속 되지 않습니다. 연락처 컨트롤러 ContactManager 서비스를 만들 때 컨트롤러 다음과 같이 해당 ModelState 래핑합니다.

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample9.cs)]

## <a name="summary"></a>요약

이 반복에 않아 응용 프로그램에는 새로운 기능을 추가 하지 않았습니다. 이 반복의 목표 하도록 쉽게 유지 관리 및 수정 하 여 Contact Manager 응용 프로그램을 리팩터링 하는 것 이었습니다.

첫째, 리포지토리 소프트웨어 디자인 패턴을 구현 했습니다. 데이터 액세스 코드를 모두 마이그레이션할 별도 ContactManager 저장소 클래스를 합니다.

우리는 컨트롤러 논리에서 유효성 검사 논리 격리. 모든 유효성 검사 코드를 포함 하는 별도 서비스 계층을 만들었는지 여부입니다. 컨트롤러 계층의 서비스 계층 상호 작용 하 고 서비스 계층은 저장소 계층 상호 작용 합니다.

서비스 계층을 만들 때의 순서로 Decorator 패턴 ModelState 우리의 서비스 계층에서 격리 합니다. 이 서비스 계층에서 ModelState 대신 IValidationDictionary 인터페이스에 대해 프로그래밍.

마지막으로,의 순서로 종속성 주입 패턴 라는 소프트웨어 디자인 패턴. 이 패턴을 구체적인 클래스가 아닌 인터페이스 (추상화)에 대해 프로그래밍할 수 있습니다. 종속성 주입 디자인 패턴을 구현 하면 코드가 더 테스트할 수 있습니다. 다음 반복에는 프로젝트에 단위 테스트 추가합니다.

> [!div class="step-by-step"]
> [이전](iteration-3-add-form-validation-cs.md)
> [다음](iteration-5-create-unit-tests-cs.md)
