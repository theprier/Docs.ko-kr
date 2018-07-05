---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
title: '반복 #6-테스트 기반 개발 (VB)를 사용 하 여. | Microsoft Docs'
author: microsoft
description: 이 여섯 번째 반복에서는 추가 새로운 기능을 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대 한 코드를 작성 합니다. 이 반복 하는 중...
ms.author: aspnetcontent
ms.date: 02/20/2009
ms.assetid: e1fd226f-3f8e-4575-a179-5c75b240333d
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
msc.type: authoredcontent
ms.openlocfilehash: f5ef03c76d1ecc72cffdeed6f8dcd1b5e39d859d
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37829274"
---
<a name="iteration-6--use-test-driven-development-vb"></a>반복 #6-사용 하 여 테스트 기반 개발 (VB)
====================
[Microsoft](https://github.com/microsoft)

[코드 다운로드](iteration-6-use-test-driven-development-vb/_static/contactmanager_6_vb1.zip)

> 이 여섯 번째 반복에서는 추가 새로운 기능을 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대 한 코드를 작성 합니다. 이 반복에서는 메일 그룹을 추가합니다.


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>연락처 관리 ASP.NET MVC 응용 프로그램을 작성 (VB)
  

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

연락처 관리자 응용 프로그램의 이전 반복에서 코드에 대 한 안전망을 제공 하는 단위 테스트를 만들었습니다. 단위 테스트를 만들기 위한 동기 코드를 변경 하려면 복원 력이 더욱 높아집니다 확인 하는 것 이었습니다. 곳에서 단위 테스트를 사용 하 여에서는 문제 없이 코드를 변경 하 고 기존 기능이 손상 여부는 곧바로 알 수 있습니다.

이 반복 단위 테스트는 완전히 다른 용도로 사용합니다. 이 반복 호출 하는 응용 프로그램 디자인 철학의 일부로 단위 테스트 사용 *테스트 기반 개발*합니다. 테스트 기반 개발을 연습 하는 경우 먼저 테스트를 작성 하 고 테스트에 대해 코드를 작성 합니다.

보다 정확 하 게 테스트 기반 개발을 실행 하는 경우 세 가지 단계 코드를 만들 때 완료 하는 (빨강 / 녹색/리팩터링):

1. 실패 (빨간색) 단위 테스트 작성
2. 단위 테스트 (녹색)를 전달 하는 코드 작성
3. (리팩터링) 코드를 리팩터링

먼저 단위 테스트를 작성 합니다. 단위 테스트 코드를 예상 하는 방법에 대 한 동작을 의도 표현 해야 합니다. 단위 테스트를 처음 만들 때 단위 테스트 실패 해야 합니다. 테스트를 충족 하는 응용 프로그램 코드를 작성 하지 않은 때문에 테스트가 실패 합니다.

다음으로 단위 테스트를 위해 충분 코드를 작성 합니다. 목표 laziest, sloppiest 및 가능한 가장 빠른 방법으로 코드를 작성 하는 것입니다. 응용 프로그램의 아키텍처에 대 한 시간 생각을 허비 하지 해야 합니다. 대신, 최소한의 단위 테스트에 의해 표현 하려는 의도 충족 하는 데 필요한 코드 작성에 집중 해야 합니다.

마지막으로 충분 한 코드를 작성 한 후 뒤로 이동 하 고 응용 프로그램의 전반적인 아키텍처 고려 수 있습니다. (리팩터링)를 다시 작성할 때이 단계에서는 소프트웨어 디자인의 장점을 활용 하 여 코드 패턴-리포지토리 패턴-같은 코드를 관리할 수 있도록 합니다. 단위 테스트에서 코드 검사는 때문에이 단계에서는 코드 거침 없이 다시 작성할 수 있습니다.

테스트 중심 개발 연습에서 발생 하는 많은 이점이 있습니다. 첫 번째 테스트 기반 개발을 강제로 실제로 작성 해야 하는 코드 작성에 집중할 수 있습니다. 특정 테스트를 통과 하는 데 충분 한 코드 작성에 지속적으로 포커스가 있는, 때문에 엄청난 양의 사용 하지는 않는 코드를 쓰고 근본 원인을 제거 들어가게에서 수 없습니다.

둘째, "먼저 테스트" 디자인 방법론을 강제로 코드를 사용 하는 방법의 관점에서 코드를 작성할 수 있습니다. 즉, 테스트 기반 개발을 실행 하는 경우 지속적으로 작성 하는 테스트 사용자 관점에서 합니다. 따라서 깔끔하고 더 이해할 수 있는 Api 테스트 기반 개발 될 수 있습니다.

마지막으로 테스트 기반 개발을 강제로 응용 프로그램을 작성 하는 일반적인 프로세스의 일부로 단위 테스트를 작성할 수 있습니다. 프로젝트 최종 기한이 가까워지면 테스트는 일반적으로 창 이동 하는 첫 번째 가장 합니다. 테스트 기반 개발을 캡처하므로 반면에 때는 테스트 기반 개발을 통해 단위 테스트 중앙 응용 프로그램을 빌드하는 프로세스 때문에 단위 테스트를 작성 하는 방법에 대 한 원동력이 될 가능성이 있습니다.

> [!NOTE] 
> 
> 테스트 기반 개발에 대 한 자세한 내용은 필자를 읽어 Michael Feathers 책 **Working Effectively with Legacy Code**합니다.


이 반복에서 연락처 관리자 응용 프로그램에 새 기능을 추가 합니다. 메일 그룹에 대 한 지원을 추가합니다. 연락처와 같은 범주로 연락처를 구성 하는 그룹 및 친구 그룹을 사용할 수 있습니다.

이 새로운 기능 테스트 기반 개발 프로세스를 수행 하 여 응용 프로그램을 추가 합니다. 먼저 단위 테스트를 작성 하 고 모든이 테스트에 대 한 코드를 작성 합니다.

## <a name="what-gets-tested"></a>어떤 테스트를 가져옵니다.

이전 반복에서 설명한 대로 일반적으로 데이터 액세스 논리에 대 한 단위 테스트를 작성 하거나 하지 논리를 확인 합니다. 데이터베이스에 액세스 하는 느린 작업 이므로 데이터 액세스 논리에 대 한 t 쓰기 단위 테스트 하지. 뷰 논리에 대 한 t 쓰기 단위 테스트 보기에 액세스 하므로 작업이 비교적 느립니다는 웹 서버를 스핀업 하지. T 해서는 테스트 매우 빠른에 반복 해 서 실행할 수 있습니다 하지 않는 한 단위 테스트를 작성

테스트 기반 개발, 단위 테스트에 고정 하기 때문에 집중 처음 컨트롤러 및 비즈니스 논리를 작성 합니다. 에서는 데이터베이스 또는 뷰를 변경 하지 마세요. T 땀이 자습서의 끝까지이 뷰를 만들거나 데이터베이스를 수정 합니다. 테스트할 무엇부터 시작 하겠습니다.

## <a name="creating-user-stories"></a>사용자 스토리 만들기

테스트 기반 개발을 실행 하는 경우 항상 테스트를 작성 하 여 시작 합니다. 즉시 질문을 제기 합니다: 먼저 작성 하는 테스트를 어떻게 결정 하나요? 이 질문에 답하기 위해 집합이 써야 [ *사용자 스토리*](http://en.wikipedia.org/wiki/User_stories)합니다.

사용자 스토리는 소프트웨어 요구 사항 (일반적으로 한 문장) 설명은 매우 간단 합니다. 사용자 관점에서 작성 하는 요구 사항에 대 한 기술적인 설명을 해야 합니다.

새 메일 그룹 기능에 필요한 기능을 설명 하는 사용자 스토리 집합 s는 다음과 같습니다.

1. 사용자 연락처 그룹 목록을 볼 수 있습니다.
2. 사용자는 새 메일 그룹을 만들 수 있습니다.
3. 기존 연락처 그룹을 삭제할 수 있습니다.
4. 새 연락처를 만들 때 사용자 연락처 그룹을 선택할 수 있습니다.
5. 기존 연락처를 편집할 때 사용자 연락처 그룹을 선택할 수 있습니다.
6. 인덱스 보기에 연락처 그룹 목록이 표시 됩니다.
7. 사용자가 연락처 그룹을 클릭 하면 일치 연락처 목록이 표시 됩니다.

이 목록은 사용자 스토리는 고객에 의해 완전히 이해할 수 인지 확인 합니다. 기술 구현 세부 정보에 대 한 언급이 없는 경우

응용 프로그램을 빌드하는 단계에서 사용자 스토리 집합을 더 구체화 될 수 있습니다. 사용자 스토리 (요구 사항) 여러 스토리로 중단할 수 있습니다. 예를 들어, 새 연락처 그룹을 만드는 해야 한다는 유효성 검사를 결정할 수 있습니다. 이름이 없는 연락처 그룹 제출 유효성 검사 오류를 반환 해야 합니다.

사용자 스토리의 목록을 만든 후 첫 번째 단위 테스트를 작성할 준비가 되었습니다. 연락처 그룹의 목록 보기에 대 한 단위 테스트를 만들어 시작 하겠습니다.

## <a name="listing-contact-groups"></a>연락처 그룹 나열

이 첫 번째 사용자 스토리 된다는 사용자는 연락처 그룹 목록을 볼 수 있습니다. 테스트를 사용 하 여이 스토리를 표현 해야 합니다.

ContactManager.Tests 프로젝트에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 여 새 단위 테스트를 만들 선택 **추가, 새 테스트**를 선택 하는 **단위 테스트** 템플릿 (그림 1 참조). 이름을 새 단위 테스트 GroupControllerTest.vb을 클릭 합니다 **확인** 단추입니다.


[![GroupControllerTest 단위 테스트를 추가합니다.](iteration-6-use-test-driven-development-vb/_static/image1.jpg)](iteration-6-use-test-driven-development-vb/_static/image1.png)

**그림 01**: GroupControllerTest 단위 테스트 추가 ([큰 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image2.png))


첫 번째 단위 테스트는 목록 1에 포함 됩니다. 이 테스트 그룹 컨트롤러의 index () 메서드 그룹 집합을 반환 하는 확인 합니다. 이 테스트는 그룹의 컬렉션은 보기에 반환 된 데이터를 확인 합니다.

**1-Controllers\GroupControllerTest.vb 나열**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample1.vb)]

목록 1 Visual Studio에서 코드를 처음 입력 하면 빨간색의 구불구불한 선 많이 받게 됩니다. 클래스는 GroupController 또는 그룹을 만들지 않았습니다.

T도 빌드가 하시면이 시점에서 응용 프로그램 t 수 있도록 첫 번째 단위 테스트를 실행 합니다. 좋은 s입니다. 실패 한 테스트로 계산합니다. 따라서 이제 응용 프로그램 코드 작성을 시작할 수 있는 권한이 있습니다. 테스트를 실행 하려면 충분 한 코드를 작성 해야 합니다.

목록 2에서 그룹 컨트롤러 클래스의 단위 테스트를 통과 하는 데 필요한 코드는 최소 사항만 포함 합니다. Index () 작업 그룹 (그룹 클래스는 목록 3에서 정의 됩니다.)의 정적으로 코딩 된 목록을 반환 합니다.

**Listing 2 - Controllers\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample2.vb)]

**3-Models\Group.vb 나열**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample3.vb)]

첫 번째 단위 테스트를 성공적으로 완료 GroupController 및 그룹 클래스를 프로젝트에 추가 했습니다 (그림 2 참조). 수행한 테스트를 통과 하는 데 필요한 최소 작업 합니다. 축 하 하기 위해 차례입니다.


[![성공 했습니다.](iteration-6-use-test-driven-development-vb/_static/image2.jpg)](iteration-6-use-test-driven-development-vb/_static/image3.png)

**그림 02**: 성공! ( [클릭 하 여 큰 이미지 보기](iteration-6-use-test-driven-development-vb/_static/image4.png))


## <a name="creating-contact-groups"></a>메일 그룹 만들기

이제 두 번째 사용자 스토리에으로 이동할 수 있습니다. 새 메일 그룹을 만들 수 해야 합니다. 테스트를 사용 하 여이 의도 표현 해야 합니다.

목록 4에서 테스트 메서드는 새 그룹을 사용 하 여 index () 메서드에 의해 반환 되는 그룹 목록에 그룹을 추가 하는 create () 호출 하는 확인 합니다. 즉, 새 그룹을 만드는 경우 다음 필자 있어야 index () 메서드에 의해 반환 되는 그룹 목록에서 새 그룹을 다시 가져오는 데 합니다.

**4-Controllers\GroupControllerTest.vb 나열**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample4.vb)]

목록 4의 테스트 그룹 컨트롤러 새 연락처 그룹을 사용 하 여 create () 메서드를 호출합니다. 다음으로 테스트 그룹 컨트롤러 index () 메서드 호출에서 반환 하는 새 그룹 데이터 보기를 확인 합니다.

수정 된 그룹 컨트롤러 목록 5에 새 테스트를 통과 하는 데 필요한 변경 하는 최소 사항만 포함 합니다.

**Listing 5 - Controllers\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample5.vb)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a>그룹 컨트롤러 목록 5의 새 create () 작업이 있습니다. 이 작업 그룹의 컬렉션에 그룹을 추가 합니다. Index () 작업 그룹 컬렉션의 내용을 반환 수정 되었다는 사실을 알 수 있습니다.

다시 한 번 최소한 단위 테스트를 통과 하는 데 필요한 작업의 수행 했습니다. 그룹 컨트롤러에 이러한 변경을 수행, 후 모든 유닛 테스트를 통과 합니다.

## <a name="adding-validation"></a>유효성 검사 추가

이 요구 사항은 사용자 스토리에 명시적으로 언급 하지. 그러나 그룹 이름에 포함 하려면 적절 한 것입니다. 그렇지 않으면 연락처를 그룹으로 구성 됩니다 하지 매우 유용 합니다.

코드 6이이 의도 표현 하는 새 테스트를 포함 합니다. 이 테스트에 유효성 검사 오류 메시지가 모델 상태에서 이름 결과 제공 하지 않고 그룹을 만들려고 하는 확인 합니다.

**Listing 6 - Controllers\GroupControllerTest.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample6.vb)]

이 테스트를 충족 하기 위해 그룹 클래스 (참조 코드 7)에 Name 속성을 추가 해야 합니다. 또한 그룹 컨트롤러 create () 작업 (참조 코드 8) s에 짤막한 유효성 검사 논리를 추가 해야 합니다.

**7-Models\Group.vb 나열**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample7.vb)]

**Listing 8 - Controllers\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample8.vb)]

이제 create () 작업 그룹 컨트롤러 논리 유효성 검사 및 데이터베이스를 모두 포함 되어 있는지 확인 합니다. 현재 그룹 컨트롤러에서 사용 하는 데이터베이스의 메모리 내 컬렉션을 이상의 아무 것도 구성 됩니다.

## <a name="time-to-refactor"></a>리팩터링 하는 시간

리팩터링 부분은 빨강/녹색/리팩터링 하는 세 번째 단계입니다. 이 시점에서 해야 코드에서 다시 실행 하 고 해당 디자인을 개선 하기 위해 응용 프로그램을 리팩터링할 수 있습니다 하는 방법을 고려해 야 합니다. 리팩터링 단계는 소프트웨어 설계 원칙과 패턴을 구현 하는 최상의 방법에 대 한 하드 생각 하는 단계 이며

코드의 디자인을 향상 하도록 선택한 어떤 방식으로든 코드를 수정할 수 있습니다. 미국 기존 기능이 망가질 하지 못하도록 하는 단위 테스트의 안전망 했습니다.

현재는 그룹 컨트롤러 좋은 소프트웨어 설계의 관점에서 교통이 복잡 합니다. 그룹 컨트롤러 상호 의존성이 높은 교통이 복잡 유효성 검사 및 데이터 액세스 코드를 포함합니다. 단일 책임 원칙을 위반을 방지 하려면 이러한 문제를 다른 클래스로 분리 해야 합니다.

리팩터링된 그룹 컨트롤러 클래스는 9 목록에 포함 됩니다. 컨트롤러는 ContactManager 서비스 계층을 사용 하도록 수정 되었습니다. 이것이 연락처 컨트롤러를 사용 하 여 사용 하는 것과 동일한 서비스 계층입니다.

코드 10 유효성 검사, 나열 및 그룹 만들기를 지원 하기 위해 ContactManager 서비스 계층에 추가 하는 새 메서드가 포함 됩니다. IContactManagerService 인터페이스는 새 메서드를 포함 하도록 업데이트 되었습니다.

코드 11 IContactManagerRepository 인터페이스를 구현 하는 새 FakeContactManagerRepository 클래스를 포함 합니다. 또한 IContactManagerRepository 인터페이스를 구현 하는 EntityContactManagerRepository 클래스와 달리 새 FakeContactManagerRepository 클래스 데이터베이스와 통신 하지 않습니다. FakeContactManagerRepository 클래스는 데이터베이스에 대 한 프록시로 메모리 내 컬렉션을를 사용합니다. 가상 repository 계층으로이 클래스는 단위 테스트에서 사용 하겠습니다.

**Listing 9 - Controllers\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample9.vb)]

**Listing 10 - Controllers\ContactManagerService.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample10.vb)]

**11-Controllers\FakeContactManagerRepository.vb 나열**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample11.vb)]


인터페이스를 사용 하려면 IContactManagerRepository 수정 하는 데 CreateGroup() 메서드와 ListGroups() EntityContactManagerRepository 클래스에서 구현 합니다. 이렇게 하려면 laziest 쉽고 빠른 방법은 다음과 같습니다. 스텁 메서드는 다음과 같은 추가 하려면

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample12.vb)]


마지막으로, 이러한 응용 프로그램의 디자인이 변경 해야 단위 테스트를 약간 수정 합니다. 이제 단위 테스트를 수행 하는 경우는 FakeContactManagerRepository를 사용 해야 합니다. 업데이트 된 GroupControllerTest 클래스 12 목록에 포함 됩니다.

**Listing 12 - Controllers\GroupControllerTest.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample13.vb)]

이러한 모든 만든 후 변경 이번에 단위 테스트 통과의 모든 됩니다. 빨강/녹색/리팩터링의 전체 주기 작업을 완료 했습니다. 첫 번째 두 개의 사용자 스토리를 구현 했습니다. 이제 사용자 스토리에 표현 된 요구 사항에 대 한 단위 테스트를 지원 했습니다. 사용자 스토리의 나머지 부분을 구현 빨강/녹색/리팩터링의 동일한 주기를 반복 하는 작업을 해야 합니다.

## <a name="modifying-our-database"></a>데이터베이스를 수정합니다.

그러나 모든 단위 테스트에서 표현 된 요구 사항을 충족 한 것에 작업 수행 되지 않습니다. 여전히 데이터베이스를 수정 해야 합니다.

새 그룹 데이터베이스 테이블을 생성 해야 합니다. 아래 단계를 수행합니다.

1. 서버 탐색기 창에서 테이블 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **새 테이블 추가**합니다.
2. 테이블 디자이너에서 아래에 설명 된 두 개의 열을 입력 합니다.
3. Id 열을 기본 키와 Id 열으로 표시 합니다.
4. 플로피의 아이콘을 클릭 하 여 그룹의 이름 사용 하 여 새 테이블을 저장 합니다.

<a id="0.12_table01"></a>


| **열 이름** | **데이터 형식** | **Null 허용** |
| --- | --- | --- |
| ID | int | False |
| name | nvarchar(50) | False |


다음으로, Contacts 테이블에서 모든 데이터를 삭제 해야 (땀이 고, 그렇지 t 연락처 및 그룹이 테이블 간의 관계를 만들 수)입니다. 아래 단계를 수행합니다.

1. Contacts 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **테이블 데이터 표시**합니다.
2. 모든 행을 삭제 합니다.

다음으로 그룹 데이터베이스 테이블 및 기존 연락처 데이터베이스 테이블 간의 관계를 정의 해야 합니다. 아래 단계를 수행합니다.

1. 테이블 디자이너를 열고 서버 탐색기 창에서 Contacts 테이블을 두 번 클릭 합니다.
2. GroupId 라는 Contacts 테이블에 새 정수 열을 추가 합니다.
3. 외래 키 관계 대화 상자를 열려면 관계 단추를 클릭 (그림 3 참조).
4. 추가 단추를 클릭 합니다.
5. 테이블 및 열 사양 단추 옆에 나타나는 줄임표 단추를 클릭 합니다.
6. 테이블 및 열 대화 상자에서 기본 키 열으로 Id와 기본 키 테이블 그룹을 선택 합니다. GroupId 외래 키 열으로 외래 키 테이블와 연락처를 선택 (그림 4 참조). 확인 단추를 클릭 합니다.
7. 아래 **INSERT 및 UPDATE 사양**에 값을 선택 **Cascade** 에 대 한 **삭제 규칙**합니다.
8. 외래 키 관계 대화 상자를 닫으려면 닫기 단추를 클릭 합니다.
9. Contacts 테이블에 변경 내용을 저장 하려면 저장 단추를 클릭 합니다.


[![데이터베이스 테이블 관계 만들기](iteration-6-use-test-driven-development-vb/_static/image3.jpg)](iteration-6-use-test-driven-development-vb/_static/image5.png)

**그림 03**: 데이터베이스 테이블 관계 만들기 ([큰 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image6.png))


[![테이블 관계를 지정합니다.](iteration-6-use-test-driven-development-vb/_static/image4.jpg)](iteration-6-use-test-driven-development-vb/_static/image7.png)

**그림 04**: 테이블 관계를 지정 합니다. ([큰 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image8.png))


### <a name="updating-our-data-model"></a>데이터 모델 업데이트

다음으로 새 데이터베이스 테이블을 나타내는 데이터 모델을 업데이트 해야 합니다. 아래 단계를 수행합니다.

1. 엔터티 디자이너를 열려면 모델 폴더에서 ContactManagerModel.edmx 파일을 두 번 클릭 합니다.
2. 디자이너의 화면을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **데이터베이스에서 모델 업데이트**합니다.
3. 업데이트 마법사에서 선택한 그룹 테이블 마침을 클릭 (그림 5 참조) 단추입니다.
4. 그룹 엔터티를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **이름 바꾸기**합니다. 이름을 변경 합니다 *그룹* 엔터티의 *그룹* (단일).
5. 연락처 엔터티 맨 아래에 표시 되는 그룹 탐색 속성을 마우스 오른쪽 단추로 클릭 합니다. 이름을 변경 합니다 *그룹* 탐색 속성을 *그룹* (단 수 화) 합니다.


[![데이터베이스에서 Entity Framework 모델을 업데이트합니다.](iteration-6-use-test-driven-development-vb/_static/image5.jpg)](iteration-6-use-test-driven-development-vb/_static/image9.png)

**그림 05**: 데이터베이스에서 Entity Framework 모델을 업데이트 ([큰 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image10.png))


다음이 단계를 완료 한 후 데이터 모델에는 연락처와 그룹 모두 테이블을 나타냅니다. Entity Designer는 엔터티를 모두 표시 됩니다 (그림 6 참조).


[![그룹 및 연락처를 표시 하는 엔터티 디자이너](iteration-6-use-test-driven-development-vb/_static/image6.jpg)](iteration-6-use-test-driven-development-vb/_static/image11.png)

**그림 06**: 그룹 및 연락처를 표시 하는 Entity Designer ([큰 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image12.png))


### <a name="creating-our-repository-classes"></a>리포지토리 클래스 만들기

그런 다음 리포지토리 클래스를 구현 해야 합니다. 이 반복 과정을 통해 추가한 새 메서드가 여러 개 IContactManagerRepository 인터페이스에 단위 테스트를 충족 하기 위해 코드를 작성 하는 동안. IContactManagerRepository 인터페이스의 최종 버전 14 목록에 포함 됩니다.

**Listing 14 - Models\IContactManagerRepository.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample14.vb)]

에서는 실제 EntityContactManagerRepository 클래스에서 연락처 그룹 작업과 관련 된 방법 중 하나는 되지 않았습니까 실제로 구현 합니다. 현재 EntityContactManagerRepository 클래스에 각 IContactManagerRepository 인터페이스에 나열 된 연락처 그룹 방법에 대 한 스텁 메서드가 있습니다. 예를 들어 ListGroups() 메서드는 현재 다음과 같이 표시 됩니다.

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample15.vb)]

스텁 메서드를 사용 하면 응용 프로그램을 컴파일 및 단위 테스트를 통과 수 있었습니다. 그러나 이제는 실제로 이러한 메서드를 구현 하는 시간 EntityContactManagerRepository 클래스의 최종 버전 13 목록에 포함 됩니다.

**Listing 13 - Models\EntityContactManagerRepository.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample16.vb)]

### <a name="creating-the-views"></a>뷰 만들기

ASP.NET MVC 응용 프로그램 기본 ASP.NET 뷰 엔진을 사용 하는 경우입니다. 따라서 don t는 특정 단위 테스트에 대 한 응답에 뷰를 만듭니다. 그러나 응용 프로그램에 정보를 보기 없으면 되므로 하시면 t를 만들어 연락처 관리자 응용 프로그램에 포함 된 뷰를 수정 하지 않고이 반복을 완료 합니다.

다음 새 뷰를 만드는 데 연락처 그룹 관리를 위한 (그림 7 참조) 해야 합니다.

- Views\Group\Index.aspx-연락처 그룹 목록 표시 합니다.
- Views\Group\Delete.aspx-연락처 그룹을 삭제 하는 것에 대 한 확인 양식 표시


[![그룹 인덱스 보기](iteration-6-use-test-driven-development-vb/_static/image7.jpg)](iteration-6-use-test-driven-development-vb/_static/image13.png)

**그림 07**: The 그룹 인덱스 보기 ([큰 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image14.png))


연락처 그룹 포함 되도록 다음 기존 뷰를 수정 해야 합니다.

- Views\Home\Create.aspx
- Views\Home\Edit.aspx
- Views\Home\Index.aspx

이 자습서와 함께 제공 되는 Visual Studio 응용 프로그램에서 확인 하 여 수정 된 보기를 볼 수 있습니다. 예를 들어, 그림 8에서는 연락처 인덱스 뷰를 보여 줍니다.


[![연락처 인덱스 보기](iteration-6-use-test-driven-development-vb/_static/image8.jpg)](iteration-6-use-test-driven-development-vb/_static/image15.png)

**그림 08**: The 연락처 인덱스 보기 ([큰 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image16.png))


## <a name="summary"></a>요약

이 반복에 추가한 새 기능 연락처 관리자 응용 프로그램 테스트 기반 개발 응용 프로그램 디자인 방법론을 수행 하 여 합니다. 사용자 스토리의 집합을 만들어 시작 합니다. 사용자 스토리에 의해 표현 된 요구 사항에 해당 하는 단위 테스트 집합을 만들었습니다. 마지막으로, 단위 테스트로 표현 된 요구 사항을 충족 하도록 충분 한 코드만 작성 되었습니다.

단위 테스트로 표현 된 요구 사항을 충족 하도록 충분 한 코드를 작성 끝나면 데이터베이스 및 뷰를 업데이트 했습니다. 데이터베이스에 새 그룹 테이블을 추가 하 고 Entity Framework 데이터 모델을 업데이트 합니다. 또한 생성 하 고 뷰 집합을 수정 합니다.

다음 반복-마지막 반복-에서는 Ajax를 활용 하도록 응용 프로그램에 다시 작성 합니다. Ajax를 활용 하 여 연락처 관리자 응용 프로그램의 성능과 응답성 개선 됩니다.

> [!div class="step-by-step"]
> [이전](iteration-5-create-unit-tests-vb.md)
> [다음](iteration-7-add-ajax-functionality-vb.md)
