---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
title: 반복 6-테스트 기반 개발 (VB)를 사용 하 여 | Microsoft Docs
author: microsoft
description: 이 6 번째 반복에서에서는 새 기능을 추가할 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대해 코드를 작성 합니다. 이 반복에...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: e1fd226f-3f8e-4575-a179-5c75b240333d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
msc.type: authoredcontent
ms.openlocfilehash: 71b3425c5ca8cbfc1b89493c7afb26681f8bdc9d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30877595"
---
<a name="iteration-6--use-test-driven-development-vb"></a>반복 6-테스트 기반 개발 (VB)를 사용 합니다.
====================
by [Microsoft](https://github.com/microsoft)

[코드 다운로드](iteration-6-use-test-driven-development-vb/_static/contactmanager_6_vb1.zip)

> 이 6 번째 반복에서에서는 새 기능을 추가할 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대해 코드를 작성 합니다. 이 반복 메일 그룹을 추가합니다.


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>연락처 관리 ASP.NET MVC 응용 프로그램 (VB) 빌드
  

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

않아 응용 프로그램의 이전 반복의 코드에 대 한 안전망을 제공 하는 단위 테스트를 만들었습니다. 단위 테스트를 만들기 위한 동기 코드를 변경 하려면 복원 성도 뛰어납니다. 확인 하는 것 이었습니다. 위치에 단위 테스트도 코드를 변경 하 고 즉시 기존 기능이 손상 여부를 알아야 수 우리 합니다.

이 반복에 완전히 다른 용도 대 한 단위 테스트 사용 합니다. 이 반복 호출 하는 응용 프로그램 디자인 원칙의 일환으로 단위 테스트 사용 *테스트 기반 개발*합니다. 테스트 기반 개발을 연습 하는 경우에 테스트를 먼저 작성 한 다음 테스트에 대 한 코드 작성 합니다.

보다 정확 하 게 테스트 기반 개발 연습 하는 경우 세 가지 단계 코드를 만들 때 완료 하는 (빨강 / 녹색/리팩터링):

1. 실패 (빨간색) 되는 단위 테스트 작성
2. 단위 테스트 (녹색)를 전달 하는 코드를 작성 합니다.
3. (리팩터링) 코드를 리팩터링

첫째, 단위 테스트를 작성 합니다. 단위 테스트 코드를 예상 하는 방법에 대 한 동작을 의도 표현 해야 합니다. 단위 테스트를 처음 만들 때 단위 테스트가 실패 해야 합니다. 테스트는 테스트를 충족 하는 모든 응용 프로그램 코드를 작성 하지 않았습니다 때문에 실패 해야 합니다.

다음으로 전달 하는 단위 테스트를 위해 충분 한 코드를 작성 합니다. 목표 laziest, sloppiest 고 가능한 가장 빠른 방법으로 코드를 작성 하는 것입니다. 응용 프로그램의 아키텍처에 대 한 시간 생각을 낭비 하지 해야 합니다. 대신, 최소한의 단위 테스트로 표현 된 설정 하려는 의도 충족 하는 데 필요한 코드를 작성에 초점을 맞추어야 합니다.

마지막으로, 충분 한 코드를 작성 한 후 실행 다시 하 고 응용 프로그램의 전반적인 아키텍처는 것이 좋습니다. 이 단계를 다시 작성 (리팩터링) 소프트웨어 디자인을 이용 하 여 코드 패턴-리포지토리 패턴-같은 코드를 더 쉽게 유지 관리할 수 있도록 합니다. 단위 테스트에서 코드 검사는 때문에이 단계에서는 코드 fearlessly 다시 작성할 수 있습니다.

테스트 기반 개발을 수행 하 여 발생 하는 많은 이점이 있습니다. 첫째, 테스트 기반 개발을 강제로 실제로 기록해 야 하는 코드에 집중할 수 있습니다. 특정 테스트를 통과 하는 데 충분 한 코드 작성에 계속 포커스가 있는, 때문에 여행 중에 나에 만난 및 대량의 결코 사용 하는 코드를 작성할 수 없습니다.

둘째, "먼저 테스트" 디자인 방법론 되도록 코드를 어떻게 사용할 것의 관점에서 코드를 작성할 수 합니다. 즉, 테스트 기반 개발 연습 지속적으로 작성 하는 경우 테스트 사용자 관점에서 합니다. 따라서 보다 명확 하 고 쉽게 Api 테스트 기반 개발 될 수 있습니다.

마지막으로, 테스트 기반 개발을 강제로 응용 프로그램을 작성 하는 일반적인 프로세스의 일부로 단위 테스트를 작성할 수 있습니다. 마감일이 다음 프로젝트에 가까워지면 테스트는 일반적으로 먼저 창의 외부로 이동 합니다. 테스트 기반 개발 연습 반면에 때는 테스트 기반 개발 하면 단위 테스트 중앙 응용 프로그램을 구축 과정에 단위 테스트를 작성 하는 방법에 대 한 원동력이 될 가능성이 높습니다.

> [!NOTE] 
> 
> 테스트 기반 개발에 대 한 자세한 내용은 것이 좋습니다. Michael 페더 책을 읽어 **작업 효과적으로 레거시 코드와 함께**합니다.


이 반복에 않아 응용 프로그램에 새 기능을 추가 합니다. 메일 그룹에 대 한 지원을 추가합니다. 비즈니스와 같은 범주로 연락처를 구성 하는 담당자 그룹 및 친구 그룹을 사용할 수 있습니다.

이 새로운 기능 테스트 기반 개발 과정을 수행 하 여 응용 프로그램을 추가 합니다. 먼저 단위 테스트 작성 합니다 및 이러한 테스트에 대 한 코드의 모든 작성 합니다.

## <a name="what-gets-tested"></a>테스트 내용을 가져옵니다.

이전 반복에서 설명한 대로 일반적으로 또는 하지 않는 데이터 액세스 논리에 대 한 단위 테스트를 작성 논리 보기. 데이터베이스에 액세스 하는 상대적으로 느린 작업 이므로 데이터 액세스 논리에 대 한 t 쓰기 단위 테스트를 하지 않은 합니다. 자신에 게 맞는 t 뷰 논리에 대 한 단위 테스트를 쓰기 때문에 보기에 액세스 하는 상대적으로 속도가 느립니다 작업 웹 서버를 회전 합니다. T 이내에 사용 해야 테스트 매우 빠르게에 반복 해 서 다시 실행할 수 있습니다 않으면 단위 테스트를 작성

테스트 기반 개발, 단위 테스트에 고정 하기 때문에 집중 처음 컨트롤러 및 비즈니스 논리를 작성 합니다. 에서는 데이터베이스 또는 뷰를 변경 하지 마십시오. T 성공한 데이터베이스를 수정 하거나이 자습서의 맨 끝까지이 뷰를 생성 합니다. 가장 먼저 테스트할 수 있습니다.

## <a name="creating-user-stories"></a>사용자 스토리 만들기

테스트 기반 개발 연습 하는 경우 항상 테스트를 작성 하 여 시작 합니다. 질문을 즉시 발생이: 어떤 테스트를 먼저 작성 어떻게 결정 합니까? 이 질문의 답 집합을 작성 해야 [ *사용자 스토리*](http://en.wikipedia.org/wiki/User_stories)합니다.

사용자 스토리가 소프트웨어 요구 사항에 매우 간단한 (일반적으로 한 문장) 설명 합니다. 사용자 관점에서 작성 하는 요구 사항에 대 한 일반적인 설명을 이어야 합니다.

여기서 s는 새 메일 그룹 기능에 필요한 기능을 설명 하는 사용자 스토리 집합:

1. 사용자 연락처 그룹 목록을 볼 수 있습니다.
2. 새 메일 그룹을 만들 수 있습니다.
3. 기존 연락처 그룹을 삭제할 수 있습니다.
4. 새 연락처를 만들 때 사용자 연락처 그룹을 선택할 수 있습니다.
5. 기존 연락처를 편집할 때 사용자 연락처 그룹을 선택할 수 있습니다.
6. 인덱스 뷰의 연락처 그룹 목록이 표시 됩니다.
7. 사용자가 메일 그룹을 클릭할 때 일치 연락처 목록이 표시 됩니다.

사용자 스토리의이 목록에는 고객이 완전히 이해할 수를 확인 합니다. 기술 구현 세부 사항 언급 되지 않습니다.

응용 프로그램을 빌드하는 단계에서 사용자 스토리 집합을 더 구체화 될 수 있습니다. (요구 사항) 여러 스토리로 사용자 스토리를 중단할 수 있습니다. 예를 들어 새 연락처 그룹을 만들면 유효성 검사 참여 시켜야 수도 있습니다. 이름이 없는 연락처 그룹 제출 유효성 검사 오류를 반환 해야 합니다.

사용자 스토리의 목록을 만든 후 첫 번째 단위 테스트를 작성할 준비가 된 것입니다. 메일 그룹의 목록 보기에 대 한 단위 테스트를 만들어 시작 합니다.

## <a name="listing-contact-groups"></a>메일 그룹 나열

이 첫 번째 사용자 스토리는 사용자 연락처 그룹 목록을 볼 수 있어야 합니다. 테스트와 함께이 스토리를 나타내는 데 필요 합니다.

ContactManager.Tests 프로젝트에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 여 새 단위 테스트 만들기 선택 하면 **추가, 새 테스트**을 선택 하 고는 **단위 테스트** 서식 파일 (그림 1 참조). 새 단위 GroupControllerTest.vb를 테스트 하 고 클릭 이름은 **확인** 단추입니다.


[![GroupControllerTest 단위 테스트를 추가합니다.](iteration-6-use-test-driven-development-vb/_static/image1.jpg)](iteration-6-use-test-driven-development-vb/_static/image1.png)

**그림 01**: GroupControllerTest 단위 테스트 추가 ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image2.png))


첫 번째 단위 테스트 목록 1에 포함 됩니다. 이 테스트 그룹 컨트롤러의 index () 메서드 그룹 집합이 있는지 확인 합니다. 테스트 그룹의 컬렉션 데이터 보기에서 반환 하 되 확인 합니다.

**Listing 1 - Controllers\GroupControllerTest.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample1.vb)]

Visual Studio에서 목록 1의 코드를 먼저 입력 빨간색의 구불구불한 선 많은 얻게 됩니다. 지금은 작성 GroupController 또는 그룹 클래스입니다.

T에도 빌드를 활용해 서이 시점에서 응용 프로그램을 활용해 서 t 하므로 첫 번째 단위 테스트를 실행 합니다. 좋은 s입니다. 실패 한 테스트로 계산합니다. 따라서에서는 이제 수 있는 권한이 응용 프로그램 코드를 작성을 시작 합니다. 이 테스트를 실행할 충분 한 코드를 작성 해야 합니다.

목록 2의 그룹 컨트롤러 클래스는 최소한의 단위 테스트를 통과 하는 데 필요한 코드를 포함 합니다. Index () 작업 그룹 (그룹 클래스 보기 3에 정의 됨)의 정적으로 코딩 된 목록을 반환 합니다.

**Listing 2 - Controllers\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample2.vb)]

**Listing 3 - Models\Group.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample3.vb)]

첫 번째 단위 테스트 성공적으로 완료 된 후 GroupController 및 그룹 클래스는 프로젝트에 추가 했습니다 (그림 2 참조). 테스트를 통과 하는 데 필요한 최소 작업의 경험 합니다. 축 하는입니다.


[![성공 했습니다!](iteration-6-use-test-driven-development-vb/_static/image2.jpg)](iteration-6-use-test-driven-development-vb/_static/image3.png)

**그림 02**: 성공! 드 ( [전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image4.png))


## <a name="creating-contact-groups"></a>메일 그룹 만들기

이제 두 번째 사용자 스토리에 이동할 수 있습니다. 새 메일 그룹을 만들 수 있도록 해야 합니다. 테스트와 함께 이러한 의도 표현 해야 합니다.

테스트 목록 4에서 새 그룹을 사용 하 여 메서드 그룹 index () 메서드에 의해 반환 된 목록에 그룹을 추가 하는 create () 호출 있는지 확인 합니다. 즉, 새 그룹을 만드는 경우 다음 I 할 수 있어야 index () 메서드에 의해 반환 된 그룹의 목록에서 새 그룹을 다시 가져옵니다.

**Listing 4 - Controllers\GroupControllerTest.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample4.vb)]

테스트 목록 4에 그룹 컨트롤러 그룹 새 연락처를 사용 하 여 create () 메서드를 호출합니다. 다음으로 테스트 그룹 컨트롤러 index () 메서드 호출에서 반환 하는 새 그룹 보기 데이터를 확인 합니다.

수정 된 그룹 컨트롤러 목록 5에 최소한의 새 테스트를 통과 하는 데 필요한 변경 내용이 포함 되어 있습니다.

**Listing 5 - Controllers\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample5.vb)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a>도메인에서 그룹 컨트롤러 목록 5의 새 create () 동작을 있습니다. 이 작업 그룹의 컬렉션에 그룹을 추가 합니다. 그룹의 컬렉션의 내용을 반환 하는 index () 동작 수정 되었다는 사실을 확인 합니다.

다시 한 번에서는 단위 테스트를 통과 하는 데 필요한 최소 운영 체제 미 설치를 수행 했습니다. 그룹 컨트롤러에 이러한 변경을 수행, 후 모든 우리의 단위 테스트를 통과 합니다.

## <a name="adding-validation"></a>유효성 검사 추가

이 요구 사항은 사용자 스토리에 명시적으로 언급 하지 합니다. 그러나 상태일 그룹 이름을 수 있어야 합니다. 그렇지 않으면 연락처를 그룹으로 구성 됩니다 매우 유용 합니다.

목록 6이이 의도 표현 하는 새 테스트를 포함 합니다. 이 테스트 확인 모델 상태의 유효성 검사 오류 메시지에 이름이 결과 제공 하지 않고 그룹 만들기를 시도 합니다.

**Listing 6 - Controllers\GroupControllerTest.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample6.vb)]

이 테스트를 충족 하기 위해 Name 속성 (참조 목록 7)에서는 그룹 클래스에 추가 해야 합니다. 또한 유효성 검사 논리의 간단한 작업이 그룹 controller s create () 동작 (8 목록 참조)에 추가 해야 합니다.

**Listing 7 - Models\Group.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample7.vb)]

**Listing 8 - Controllers\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample8.vb)]

유효성 검사와 데이터베이스 논리 그룹 컨트롤러 create () 동작을 지금에 포함 되어 있는지 확인 합니다. 현재 그룹 컨트롤러에서 사용 되는 데이터베이스는 메모리 내 컬렉션에 다르지 이루어져 있습니다.

## <a name="time-to-refactor"></a>리팩터링 하는 시간

빨강/녹색/리팩터링 하는 세 번째 단계는 리팩터링 부분입니다. 이 시점에서 응용 프로그램의 디자인을 개선 하기 위해 리팩터링할 수 있습니다 어떻게 하는 것이 좋습니다.를 코드에서 다시 실행 해야 합니다. 리팩터링 단계는을 소프트웨어 디자인 원칙 및 패턴을 구현 하는 가장 좋은 방법은 대 한 하드 생각 하는 단계입니다.

코드의 디자인을 개선 하기 위해 선택 하는 코드를 수정할 수 있습니다. 기존 기능을 분리 us를 방해 하는 단위 테스트의 안전망 개가 있습니다.

지금 바로 사용, 그룹 controller은 잘 설계 된 소프트웨어의 관점에서 정리가 합니다. 그룹 컨트롤러 유효성 검사 및 데이터 액세스 코드의 혼란된 정리가 포함 되어 있습니다. 단일 책임 원칙을 위반을 방지 하려면 다양 한 클래스에 이러한 문제를 분리 해야 합니다.

리팩터링된 그룹 컨트롤러 클래스 목록 9에 포함 됩니다. 컨트롤러는 ContactManager 서비스 계층을 사용 하도록 수정 되었습니다. 연락처 컨트롤러와 사용 하는 동일한 서비스 계층입니다.

목록 10 유효성 검사, 나열 및 그룹 만들기를 지원 하기 위해 ContactManager 서비스 계층에 추가 된 새 메서드가 포함 되어 있습니다. IContactManagerService 인터페이스는 새 메서드를 포함 하도록 업데이트 되었습니다.

목록 11 IContactManagerRepository 인터페이스를 구현 하는 새 FakeContactManagerRepository 클래스를 포함 합니다. 또한 IContactManagerRepository 인터페이스를 구현 하는 EntityContactManagerRepository 클래스와 달리 새 FakeContactManagerRepository 클래스는 데이터베이스와 통신 하지 않습니다. FakeContactManagerRepository 클래스는 데이터베이스에 대 한 프록시로 메모리 내 컬렉션을 사용합니다. 이 단위 테스트에서이 클래스 가짜 저장소 계층으로 사용 합니다.

**Listing 9 - Controllers\GroupController.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample9.vb)]

**Listing 10 - Controllers\ContactManagerService.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample10.vb)]

**Listing 11 - Controllers\FakeContactManagerRepository.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample11.vb)]


인터페이스 필요 IContactManagerRepository 수정 하는 데 EntityContactManagerRepository 클래스에서 CreateGroup() 및 ListGroups() 메서드를 구현 합니다. 이렇게 하려면 laziest 및 가장 빠른 방법은 스텁 메서드는 다음과 같은 추가 하기 위해입니다.

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample12.vb)]


마지막으로, 이러한 변경 내용은 응용 프로그램의 디자인에 단위 테스트를 약간 수정을 만드는 데 필요 합니다. 이제 단위 테스트를 수행할 때의 FakeContactManagerRepository를 사용 해야 합니다. 업데이트 된 GroupControllerTest 클래스 12 목록에 포함 됩니다.

**Listing 12 - Controllers\GroupControllerTest.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample13.vb)]

이러한 모든 하도록 한 후 변경 다시 한 번 모두 우리의 단위 테스트 통과 됩니다. 빨강/녹색/리팩터링의 전체 주기를 완료 했습니다. 처음 두 개의 사용자 스토리 구현 했습니다. 이제 사용자 스토리에 명시 된 요구 사항을 대 한 단위 테스트를 지원 했습니다. 사용자 스토리의 나머지 부분에서는 구현 빨강/녹색/리팩터링의 동일한 사이클을 반복 하는 작업을 해야 합니다.

## <a name="modifying-our-database"></a>데이터베이스 수정

그러나 우리 모든 단위 테스트에서 명시 된 요구 사항을 충족 않은 경우에 작업 수행 되지는 않습니다. 여전히이 데이터베이스를 수정 해야 합니다.

새 그룹 데이터베이스 테이블을 만들려면 해야 합니다. 아래 단계를 수행합니다.

1. 서버 탐색기 창에서 테이블 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **새 테이블 추가**합니다.
2. 테이블 디자이너에서 아래에 설명 된 두 개의 열을 입력 합니다.
3. Id 열 primary key와 Id 열을 표시 합니다.
4. 이름 그룹이 포함 된 플로피 아이콘을 클릭 하 여 새 테이블을 저장 합니다.

<a id="0.12_table01"></a>


| **열 이름** | **데이터 형식** | **Null 허용** |
| --- | --- | --- |
| ID | int | False |
| 이름 | nvarchar(50) | False |


다음으로 Contacts 테이블에서 모든 데이터를 삭제 해야 (성공한 그렇지 않으면 t 연락처 및 그룹이 테이블 간의 관계를 만들 수)입니다. 아래 단계를 수행합니다.

1. Contacts 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **테이블 데이터 표시**합니다.
2. 모든 행을 삭제 합니다.

다음으로 그룹 데이터베이스 테이블 및 기존 연락처 데이터베이스 테이블 간의 관계를 정의 해야 합니다. 아래 단계를 수행합니다.

1. 테이블 디자이너를 열고 서버 탐색기 창에서 Contacts 테이블을 두 번 클릭 합니다.
2. GroupId 라는 Contacts 테이블에 새 정수 열을 추가 합니다.
3. 외래 키 관계 대화 상자를 열려면 관계 단추 클릭 (그림 3 참조).
4. 추가 단추를 클릭 합니다.
5. 테이블 및 열 사양 단추 옆에 있는 줄임표 단추를 클릭 합니다.
6. 테이블 및 열 대화 상자에서 기본 키 테이블 및 기본 키 열으로 Id로 그룹을 선택 합니다. 외래 키 테이블과 외래 키 열으로 GroupId로 연락처를 선택 (그림 4 참조). 확인 단추를 클릭 합니다.
7. 아래 **INSERT 및 UPDATE 사양**, 값을 선택 **Cascade** 에 대 한 **삭제 규칙**합니다.
8. 외래 키 관계 대화 상자를 닫고 닫기 단추를 클릭 합니다.
9. Contacts 테이블에 변경 내용을 저장 하려면 저장 단추를 클릭 합니다.


[![데이터베이스 테이블 관계 만들기](iteration-6-use-test-driven-development-vb/_static/image3.jpg)](iteration-6-use-test-driven-development-vb/_static/image5.png)

**그림 03**: 데이터베이스 테이블 관계 만들기 ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image6.png))


[![테이블 관계를 지정합니다.](iteration-6-use-test-driven-development-vb/_static/image4.jpg)](iteration-6-use-test-driven-development-vb/_static/image7.png)

**그림 04**: 테이블 관계 지정 ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image8.png))


### <a name="updating-our-data-model"></a>데이터 모델 업데이트

다음으로 새 데이터베이스 테이블을 나타내기 위해 데이터 모델을 업데이트 해야 합니다. 아래 단계를 수행합니다.

1. 엔터티 디자이너를 열려면 모델 폴더에서 ContactManagerModel.edmx 파일을 두 번 클릭 합니다.
2. 디자이너 화면을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **데이터베이스에서 모델 업데이트**합니다.
3. 업데이트 마법사는 테이블 그룹과 마침을 클릭 선택 (그림 5 참조) 단추입니다.
4. 그룹 엔터티를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **이름 바꾸기**합니다. 이름을 변경 하는 *그룹* 엔터티를 *그룹* (단 수)입니다.
5. 연락처 엔터티 맨 아래에 표시 되는 그룹 탐색 속성을 마우스 오른쪽 단추로 클릭 합니다. 이름을 변경 하는 *그룹* 탐색 속성을 *그룹* (단 수)입니다.


[![데이터베이스에서 Entity Framework 모델을 업데이트합니다.](iteration-6-use-test-driven-development-vb/_static/image5.jpg)](iteration-6-use-test-driven-development-vb/_static/image9.png)

**그림 05**: 데이터베이스에서 Entity Framework 모델을 업데이트 ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image10.png))


다음이 단계를 완료 한 후 데이터 모델에는 연락처와 그룹에 모두 테이블을 나타냅니다. 엔터티 디자이너에는 두 엔터티 표시 됩니다 (그림 6 참조).


[![엔터티 디자이너 그룹 및 연락처를 표시 합니다.](iteration-6-use-test-driven-development-vb/_static/image6.jpg)](iteration-6-use-test-driven-development-vb/_static/image11.png)

**그림 06**: 그룹 및 연락처를 표시 하는 Entity Designer ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image12.png))


### <a name="creating-our-repository-classes"></a>저장소 클래스 만들기

다음으로, 저장소 클래스를 구현 해야 합니다. 반복이 진행 되는 동안 새 메서드가 여러 개에 추가한 IContactManagerRepository 인터페이스 단위 테스트를 충족 하기 위해 코드를 작성 하는 동안 합니다. IContactManagerRepository 인터페이스의 최종 버전 14 목록에 포함 됩니다.

**Listing 14 - Models\IContactManagerRepository.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample14.vb)]

에서는 실제 EntityContactManagerRepository 클래스에 대 한 메일 그룹 작업과 관련 된 방법 중 하나는 되지 않았습니까 실제로 구현 합니다. 현재 EntityContactManagerRepository 클래스에 각 IContactManagerRepository 인터페이스에 나열 된 메일 그룹 방법의 스텁을 메서드가 있습니다. 예를 들어 ListGroups() 메서드는 현재 다음과 같이 보입니다.

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample15.vb)]

스텁 메서드를 사용 하면 응용 프로그램을 컴파일 및 단위 테스트를 통과할 수 있었습니다. 그러나 이제 속도가 실제로 이러한 메서드를 구현 합니다. EntityContactManagerRepository 클래스의 최종 버전 목록 13에 포함 됩니다.

**Listing 13 - Models\EntityContactManagerRepository.vb**

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample16.vb)]

### <a name="creating-the-views"></a>보기 만들기

ASP.NET MVC 응용 프로그램 기본 ASP.NET 뷰 엔진을 사용 하는 경우입니다. 따라서 don t는 특정 단위 테스트에 대 한 응답에 뷰를 만듭니다. 그러나 응용 프로그램 뷰 없이 쓸모 없게, 때문에 활용해 서 t를 만들고 연락처 관리자 응용 프로그램에 포함 된 뷰를 수정 하지 않고이 반복을 완료 합니다.

뷰를 만드는 다음과 같은 새 메일 그룹을 관리 하기 위한 (그림 7 참조) 해야 합니다.

- Views\Group\Index.aspx-연락처 그룹의 목록 표시 합니다.
- Views\Group\Delete.aspx-연락처 그룹을 삭제 하기 위한 표시 확인 양식


[![그룹 인덱스 보기](iteration-6-use-test-driven-development-vb/_static/image7.jpg)](iteration-6-use-test-driven-development-vb/_static/image13.png)

**그림 07**: The 그룹 인덱스 보기 ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image14.png))


메일 그룹 포함 되도록 다음 기존 뷰를 수정 해야 합니다.

- Views\Home\Create.aspx
- Views\Home\Edit.aspx
- Views\Home\Index.aspx

이 자습서와 함께 제공 하는 Visual Studio 응용 프로그램을 확인 하 여 수정 된 보기를 볼 수 있습니다. 예를 들어 그림 8에서는 연락처 인덱스 뷰를 보여 줍니다.


[![연락처 인덱스 뷰](iteration-6-use-test-driven-development-vb/_static/image8.jpg)](iteration-6-use-test-driven-development-vb/_static/image15.png)

**그림 08**: The 연락처 인덱스 보기 ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-vb/_static/image16.png))


## <a name="summary"></a>요약

이 반복에 추가 했습니다 새로운 기능 않아 응용 프로그램에서 테스트 기반 개발 응용 프로그램 디자인 방법을 따라. 사용자 스토리 집합을 만들어 시작 했습니다. 사용자 스토리에서 명시 된 요구 사항을에 해당 하는 단위 테스트 집합이 만들었는지 여부입니다. 마지막으로, 단위 테스트에 명시 된 요구 사항을 충족 하는 데 충분 한 코드를 작성 합니다.

단위 테스트에 명시 된 요구 사항을 충족 하기 위해 충분 한 코드 작성를 완료 한 후이 데이터베이스 및 뷰 업데이트 되었습니다. 데이터베이스에 새 그룹 테이블을 추가 하 고 우리의 Entity Framework 데이터 모델을 업데이트 합니다. 또한 생성 하 고 뷰 집합을 수정 합니다.

-마지막 반복-다음 반복에서 Ajax 활용 하기 위해 응용 프로그램 다시 작성 합니다. Ajax 활용 함으로써 않아 응용 프로그램의 성능 및 응답성을 향상 합니다 했습니다.

> [!div class="step-by-step"]
> [이전](iteration-5-create-unit-tests-vb.md)
> [다음](iteration-7-add-ajax-functionality-vb.md)
