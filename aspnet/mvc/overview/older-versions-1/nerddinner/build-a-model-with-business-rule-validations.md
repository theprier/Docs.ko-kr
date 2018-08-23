---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: 비즈니스 규칙 유효성 검사를 사용 하 여 모델 빌드 | Microsoft Docs
author: microsoft
description: 3 단계에는 두 쿼리를 사용 하 여 고 NerdDinner 응용 프로그램 데이터베이스를 업데이트할 수 있습니다는 모델을 만드는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: b735c414c629b9ff6617dbf80782d57543306c00
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838322"
---
<a name="build-a-model-with-business-rule-validations"></a>비즈니스 규칙 유효성 검사를 사용 하 여 모델 빌드
====================
[Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 이 무료의 3 단계 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.
> 
> 3 단계에는 두 쿼리를 사용 하 여 고 NerdDinner 응용 프로그램 데이터베이스를 업데이트할 수 있습니다는 모델을 만드는 방법을 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.


## <a name="nerddinner-step-3-building-the-model"></a>NerdDinner 단계 3: 모델 작성

모델-뷰-컨트롤러 프레임 워크에서 "모델" 라는 용어와 유효성 검사 및 비즈니스 규칙을 통합 하는 해당 도메인 논리 뿐만 아니라 응용 프로그램의 데이터를 나타내는 개체를 가리킵니다. MVC 기반 응용 프로그램의 여러 가지 "핵심" 점에서 모델과 근본적으로 나중에 볼 수 있겠지만 드라이브의 동작입니다.

모든 데이터 액세스 기술을 사용 하 여 ASP.NET MVC 프레임 워크 지원 및 개발자는 다양 한 포함 하 여 해당 모델을 구현 하는 다양 한.NET 데이터 옵션 중에서 선택할 수 있습니다: LINQ to Entities, LINQ to SQL, NHibernate, LLBLGen Pro, SubSonic, WilsonORM, 또는 원시 ADO. NET DataReaders 또는 데이터 집합입니다.

NerdDinner 응용 프로그램에 대 한 데이터베이스 디자인을 상당히 충실히 따른 것에 해당 하 고 일부 사용자 지정 유효성 검사 논리 및 비즈니스 규칙을 추가 하는 간단한 모델을 만들려면 LINQ to SQL 사용 하려고 합니다. 그런 다음 구현 추상 제거는 저장소 클래스는 데이터 지 속성 구현을 쉽게 단위를 테스트할 수 있도록 확인 하 고 응용 프로그램의 나머지 부분에서.

### <a name="linq-to-sql"></a>LINQ to SQL

LINQ to SQL은.NET 3.5의 일부로 제공 되는 ORM (개체 관계형 매퍼)입니다.

LINQ to SQL 사용을 손쉽게 데이터베이스 테이블에 맞게 코딩할 수에서는.NET 클래스를 매핑할 수 있습니다. NerdDinner 응용 프로그램에 대 한 사용 하겠습니다 것 Dinner 및 RSVP 클래스에는 데이터베이스 내에서 Dinners 테이블과 RSVP를 매핑합니다. Dinners 및 RSVP 테이블의 열은 Dinner 및 RSVP 클래스의 속성에 대응 됩니다. 각 Dinner 및 RSVP 개체는 데이터베이스의 Dinners 또는 RSVP 테이블 내에서 별도 행을 나타냅니다.

LINQ to SQL 사용 하면 SQL 문을 검색 하 고 Dinner 및 RSVP 업데이트를 수동으로 생성할 필요가 없도록 하려면 데이터베이스 데이터를 사용 하 여 개체입니다. 대신에 매핑하는 방법/데이터베이스 및 이들 간의 관계에서 Dinner 및 RSVP 클래스를 정의 하겠습니다. LINQ to SQL가 상호 작용 하 고 사용에 런타임에 사용 하려면 적절 한 SQL 실행 논리를 생성 합니다. 처리 한 다음 됩니다.

VB와 C#에서 LINQ 언어 지원 Dinner 및 RSVP를 검색 하는 표현 쿼리 작성을 사용 하 여 데이터베이스의 개체입니다. 를 작성 해야 하는 데이터 코드의 양을 최소화 하 고 깔끔한 응용 프로그램을 빌드할 수 있습니다.

### <a name="adding-linq-to-sql-classes-to-our-project"></a>이 프로젝트에 LINQ to SQL 클래스 추가

에서는 프로젝트 내에서 "Models" 폴더를 마우스 오른쪽 단추로 클릭 하 여 시작 하 고 선택 합니다 **추가-&gt;새 항목** 메뉴 명령:

![](build-a-model-with-business-rule-validations/_static/image1.png)

"새 항목 추가" 대화 상자가 표시 됩니다. "데이터" 범주별으로 필터링 하 고 그 안에 "LINQ to SQL Classes" 템플릿을 선택 하겠습니다.

![](build-a-model-with-business-rule-validations/_static/image2.png)

"NerdDinner" 항목의 이름을 하 고 "추가" 단추를 클릭 합니다. Visual Studio 우리의 \Models 디렉터리 NerdDinner.dbml 파일을 추가 하 고 LINQ to SQL 개체 관계형 디자이너를 엽니다.

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a>LINQ to SQL 사용 하 여 데이터 모델 클래스 만들기

LINQ to SQL 기존 데이터베이스 스키마에서 데이터 모델 클래스를 빠르게 만들 수 있습니다. 할 일에 모델링 하고자 하는이 서버 탐색기에서 NerdDinner 데이터베이스를 열 수 고 테이블을 선택 합니다.

![](build-a-model-with-business-rule-validations/_static/image4.png)

에서는 다음 끌 수 테이블 LINQ SQL 디자이너 화면입니다. 이 LINQ to SQL 수행할 때 Dinner 자동으로 만들어집니다 (데이터베이스 테이블 열에 매핑되는 클래스 속성)을 가진 테이블의 스키마를 사용 하 여 RSVP 클래스 및:

![](build-a-model-with-business-rule-validations/_static/image5.png)

기본적으로 LINQ to SQL 디자이너 자동으로 "이름을 복수화 할 것인지" 테이블 및 열을 데이터베이스 스키마를 기반으로 하는 클래스를 만들 때. 예를 들어: 위의 예에서 "Dinners" 테이블 "Dinner" 클래스에서 발생 합니다. 이 클래스 이름은 모델을.NET 명명 규칙을 사용 하 여 일관 되 게 주며 일반적으로 필자는 해당 요소가 있으면 디자이너 수정 편리 하 게 구성 (특히 추가할 때 테이블에 많은). 클래스 또는 항상 재정의 하 고 원하는 이름으로 변경할 수 있지만 디자이너를 생성 하는 속성의 이름 마음에 들지 않는 경우입니다. 이렇게 하려면 엔터티/속성 이름에-줄 디자이너 내에서 편집 하거나 속성 표를 통해 수정 하 여 합니다.

LINQ to SQL 디자이너도 테이블의 기본 키/외래 키 관계를 검사 하 고 자동으로 그에 따라 기본으로 기본을 만들면 다른 모델 클래스 간에 "관계 연결을 만듭니다. RSVP 테이블 Dinners 테이블에 외래 키가 있다는 사실에 따라 때 우리는 Dinners 끌어서 RSVP 둘 사이 일 대 다 관계 연결을 LINQ to SQL 디자이너에 테이블 유추 된 예를 들어, (이에 화살표로 표시 됩니다는 디자이너):

![](build-a-model-with-business-rule-validations/_static/image6.png)

위의 연결 하면 LINQ to SQL 개발자 지정된 RSVP 연관 저녁에 액세스 하는 데 사용할 수 있는 RSVP 클래스에는 강력한 형식의 "Dinner" 속성을 추가 하려면. 개발자가 검색 하 고 특정 Dinner 연관 RSVP 개체를 업데이트할 수 있도록 "RSVPs" 컬렉션 속성이 Dinner 클래스도 발생 합니다.

아래 새 RSVP 개체를 만들고 Dinner의 않으십니까 컬렉션에 추가 하는 경우 Visual Studio 내의 intellisense의 예제를 볼 수 있습니다. LINQ to SQL 자동으로 추가 방법을 "않으십니까" 컬렉션 Dinner 개체에 알 수 있습니다.

![](build-a-model-with-business-rule-validations/_static/image7.png)

RSVP 개체는 Dinner 않으십니까 컬렉션에 추가 하 여 알려주고 있습니다 LINQ to SQL Dinner 및 데이터베이스에 RSVP 행의 외래 키 관계를 연결할:

![](build-a-model-with-business-rule-validations/_static/image8.png)

하는 방법에 모델링 디자이너나 테이블 연결을 명명 된, 마음에 들지 않는 경우에이 재정의할 수 있습니다. 디자이너 내에서 연결 화살표를 클릭 하 고 이름 바꾸기, 삭제 또는 수정 하려면 속성 표를 통해 해당 속성에 액세스 합니다. NerdDinner 응용 프로그램에서 기본 연결 규칙에서는 작성 하는 데이터 모델 클래스는 잘 작동 하지만 및 기본 동작을 바로 사용할 수 있습니다.

### <a name="nerddinnerdatacontext-class"></a>NerdDinnerDataContext 클래스

Visual Studio는 자동으로 모델 및 LINQ to SQL 디자이너를 사용 하 여 정의 하는 데이터베이스 관계를 나타내는.NET 클래스를 만듭니다. 각 LINQ to SQL 디자이너 파일을 솔루션에 추가 대 한 LINQ to SQL DataContext 클래스도 생성 됩니다. LINQ to SQL 클래스 항목 "NerdDinner" 라는 것 때문에 생성 된 DataContext 클래스 이름은 "NerdDinnerDataContext"입니다. 이 NerdDinnerDataContext 클래스 방법은 주 데이터베이스와 상호 작용할 것입니다.

NerdDinnerDataContext 클래스는 데이터베이스 내에서 모델링에서는 두 테이블을 나타내는 "Dinners" 및 "RSVPs"-두 속성을 노출 합니다. 에서는 C# 하 여 데이터베이스에서 쿼리 및 검색 Dinner 및 RSVP 개체에 해당 속성에 대해 LINQ 쿼리를 작성 합니다.

다음 코드는 NerdDinnerDataContext 개체를 인스턴스화하고 Dinners 나중에 발생 하는 시퀀스에 대해 LINQ 쿼리를 수행 하는 방법을 보여 줍니다. LINQ 쿼리를 작성할 때 visual Studio는 완전 한 intellisense를 제공 하 고에서 반환 된 개체는 강력한 intellisense도 지원.

![](build-a-model-with-business-rule-validations/_static/image9.png)

Dinner 및 RSVP 개체에 대 한 쿼리 수, 하는 것 외에도 NerdDinnerDataContext도 자동으로 변경 했습니다 이후에를 통해 검색 된 Dinner 및 RSVP 개체를 추적 합니다. 데이터베이스에 다시-명시적 SQL 업데이트 코드를 작성할 필요 없이 변경 내용을 쉽게 저장 하려면이 기능을 사용할 수 있습니다.

예를 들어 아래 코드는 LINQ 쿼리를 사용 하 여, 데이터베이스에서 단일 Dinner 개체를 검색 하 고, Dinner 속성 중 두 가지를 업데이트 하 고, 다음 변경 내용을 다시 데이터베이스에 저장 하는 방법에 설명 합니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

위의 코드에서 NerdDinnerDataContext 개체에서 검색 했던 Dinner 개체에 대 한 속성 변경 내용을 자동으로 추적 됩니다. "SubmitChanges()" 메서드를 호출 하는 경우에 다시 업데이트 된 값을 유지 하려면 데이터베이스에 적절 한 SQL "업데이트" 문을 실행 합니다 것입니다.

### <a name="creating-a-dinnerrepository-class"></a>DinnerRepository 클래스 만들기

작은 응용 프로그램에 대 한 경우가 컨트롤러 LINQ to SQL DataContext 클래스에 대해 직접 작업 및 컨트롤러 내에서 LINQ 쿼리를 포함 하도록 세밀 하 게 합니다. 그러나 응용 프로그램 크기가 더 커질,이 방법은 유지 관리 하 고 테스트 하기가 불편 집니다. 여러 위치에서 동일한 LINQ 쿼리를 복제 우리에 게 발생할 수도 있습니다.

응용 프로그램 유지 관리 및 테스트를 쉽게 만들 수 있는 한 가지 방법은 "리포지토리" 패턴을 사용 하는 것입니다. 저장소 클래스는 응용 프로그램에서 데이터 지 속성의 구현 세부 요약 떨어진 데이터 쿼리 및 지 속성 논리를 캡슐화 하는 데 도움이 됩니다. 응용 프로그램 코드를 더 깔끔하게 만들 뿐 아니라 리포지토리 패턴을 사용 하 여 쉽게 데이터 저장소 구현을 나중에 변경할 수 하 고 수 단위는 실제 데이터베이스를 요구 하지 않고 응용 프로그램 테스트를 용이 하 게 하는 데 도움이 합니다.

NerdDinner 응용 프로그램에 대 한 DinnerRepository 클래스 정의 서명 아래:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

*참고:이 장 뒷부분에서에서는이 클래스에서 IDinnerRepository 인터페이스를 추출 하 고이 컨트롤러에서이 사용 하 여 종속성 주입을 사용 하도록 설정 합니다. 시작 하려면 그러나 비슷하며 간단 하 게 시작 하 고 DinnerRepository 클래스와 직접 작동 합니다.*

에서는 "Models" 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택이 클래스를 구현 하는 **추가-&gt;새 항목** 메뉴 명령입니다. "새 항목 추가" 대화 상자 내에서 "Class" 템플릿을 선택 하 고 "DinnerRepository.cs" 파일 이름:

![](build-a-model-with-business-rule-validations/_static/image10.png)

그런 다음 아래 코드를 사용 하 여 DinnerRespository 클래스를 구현할 수 있습니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a>검색, 업데이트, 삽입 및 DinnerRepository 클래스를 사용 하 여 삭제

DinnerRepository 클래스를 만들었으므로 이제이 사용 하 여 수행할 수 있습니다 일반 작업을 보여 주는 몇 가지 코드 예제에 대해 살펴보겠습니다.

#### <a name="querying-examples"></a>쿼리 예제

아래 코드는 단일 Dinner DinnerID 값을 사용 하 여 검색 합니다.


[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

아래 코드에 대해 모든 향후 dinners 및 루프를 검색합니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a>삽입 및 업데이트 예제

아래의 코드 두 개의 새 dinners를 추가 하는 방법을 보여 줍니다. 리포지토리에 추가/수정 되지에 "save ()" 메서드를 호출할 때까지 데이터베이스에 커밋되지 않습니다. LINQ to SQL 자동 줄 바꿈되어 모든 변경 내용을 데이터베이스 트랜잭션을 – 모든 변경 내용은 또는 리포지토리에서 저장할 때 하나도 수행 되므로:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

아래 코드는 기존 Dinner 개체를 검색 하 고 두 속성을 수정 합니다. 리포지토리에서 "save ()" 메서드는 호출 될 때 내용이 다시 데이터베이스에 커밋되기:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

아래 코드는 dinner 가져오고에 RSVP를 추가 합니다. 않으십니까 컬렉션 (사이의 때문에 기본 키/외래 키 관계를 데이터베이스에 두) LINQ to SQL 생성 하는 Dinner 개체에서 사용 하 여이 수행 합니다. 이 변경 "save ()" 메서드를 호출 될 때 다시 데이터베이스에 새 RSVP 테이블 행을으로 유지 됩니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a>Delete 예제

아래 코드는 기존 Dinner 개체를 검색 한 다음 삭제를 표시 합니다. "Save ()" 메서드를 호출 될 때 데이터베이스에 다시 삭제를 커밋 됩니다 것:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a>모델 클래스를 사용 하 여 유효성 검사 및 비즈니스 규칙 논리를 통합

유효성 검사 및 비즈니스 규칙 논리는 데이터와 함께 작동 하는 모든 응용 프로그램의 핵심 부분을 통합 합니다.

#### <a name="schema-validation"></a>스키마 유효성 검사

LINQ to SQL 디자이너를 사용 하 여 모델 클래스를 정의 데이터 모델 클래스의 속성 데이터 형식을 데이터베이스 테이블의 데이터 형식에 해당 합니다. 예를 들어: "datetime" Dinners 표의 "EventDate" 열을 사용 하는 경우 LINQ to SQL에서 만든 데이터 모델 클래스 형식 (즉, 기본 제공.NET 데이터 형식) "DateTime" 됩니다. 즉, 되도록 코드에서 정수 또는 부울 값을 할당 하 고 런타임 시에 유효 하지 않은 문자열 형식을 암시적으로 변환 하려고 하면 오류가 자동으로 발생 합니다 하는 경우 컴파일 오류가 발생 합니다.

문자열-는 사용자를 보호 SQL 주입 공격을 사용 하는 경우를 사용 하는 경우 LINQ to SQL 이스케이프 SQL 값을 처리도 자동으로 됩니다.

#### <a name="validation-and-business-rule-logic"></a>유효성 검사 및 비즈니스 규칙 논리

스키마 유효성 검사는 첫 번째 단계에서는 유용 하지만 거의 부족 합니다. 대부분의 실제 시나리오에서는 여러 속성에 걸쳐, 코드를 실행 하 고 모델의 상태에 대 한 인식을 경우가 수 있는 다양 한 유효성 검사 논리를 지정 하는 기능 (예:이 만들어지고/업데이트/삭제 되거나 도메인별 상태 내에서 예: "보관"). 다양 한 패턴을 정의 하 고 모델 클래스에 유효성 검사 규칙을 적용할 수 있는 프레임 워크는 여러 가지가 되며 여러.NET 기반 프레임 워크 들이 하는 데 사용할 수 있는 합니다. 거의 모든 ASP.NET MVC 응용 프로그램 내에서 사용할 수 있습니다.

NerdDinner 응용 프로그램에서는 사용 비교적 간단 하 고 직관적인 패턴을 여기서은 Dinner 모델 개체에는 IsValid 속성 및 GetRuleViolations() 메서드를 노출 합니다. IsValid 속성은 유효성 검사 및 비즈니스 규칙은 모두 유효 따라 true 또는 false를 반환 합니다. GetRuleViolations() 메서드는 모든 규칙 오류 목록을 반환 합니다.

프로젝트에 "부분 클래스"를 추가 하 여 IsValid 및 GetRuleViolations() Dinner 모델에 대 한 구현 됩니다. Partial 클래스 메서드/속성/이벤트 (예: LINQ to SQL 디자이너에서 생성 되는 Dinner 클래스)는 VS 디자이너에서 유지 관리 하는 클래스를 추가 하려면 사용할 수 있으며 도구에서 코드를 사용 하 여 작업 하는 것을 방지 합니다. 에서는 \Models 폴더를 마우스 오른쪽 단추로 클릭 하 여 프로젝트에 새로운 partial 클래스를 추가 하 고 "새 항목 추가" 메뉴 명령을 선택 합니다. "새 항목 추가" 대화 상자 내에서 "클래스" 템플릿을 선택 하 고 Dinner.cs 이름을 다음 했습니다.

![](build-a-model-with-business-rule-validations/_static/image11.png)

"추가" 단추를 클릭 Dinner.cs 파일을 프로젝트에 추가 되며 IDE 내에서 엽니다. 사용 하 여 기본 규칙/유효성 검사 적용 프레임 워크를 구현할 수 것은 아래 코드:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

위의 코드에 대 한 몇 가지 참고 사항:

- 즉, 그 안에 포함 된 코드를 LINQ to SQL 디자이너에서 생성 하 고 유지 하는 클래스를 사용 하 여 결합 되며 단일 클래스로 컴파일된 "부분" 키워드 – Dinner 클래스 앞입니다.
- RuleViolation 클래스가 규칙 위반에 대 한 자세한 세부 정보를 제공할 수 있도록 프로젝트에 추가 하는 도우미 클래스가입니다.
- Dinner.GetRuleViolations() 메서드를 호출 하면이 유효성 검사 및 비즈니스 규칙을 평가할 (구현 하 고 잠시 후). 그런 다음 시퀀스를 반환 다시 RuleViolation 개체는 모든 규칙 오류에 대 한 자세한 정보를 제공 합니다.
- Dinner.IsValid 속성 Dinner 개체에 모든 활성 RuleViolations 있는지 여부를 나타내는 편리한 도우미 속성을 제공 합니다. 언제 든 지 Dinner 개체를 사용 하 여 개발자가 사전에 확인할 수 있습니다 (고 예외가 발생 하지 않습니다).
- Dinner.OnValidate() 부분 메서드 Dinner 개체가 데이터베이스 내에서 유지 하려고 합니다. 언제 든 지 알림을 받을 수 있도록 하는 LINQ to SQL에서 제공 하는 후크 됩니다. 위의 OnValidate() 구현 Dinner에 없는 RuleViolations 저장 하기 전에 확인 합니다. 잘못 된 상태에 있으면 하면 LINQ to SQL 트랜잭션이 중단 되는 예외를 발생 시킵니다.

이 방법은 유효성 검사 및 비즈니스 규칙에 통합 수 있는 간단한 프레임 워크를 제공 합니다. 이제 추가 해 보겠습니다는 아래이 GetRuleViolations() 방법 규칙:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

모든 RuleViolations의 시퀀스를 반환 하도록 C#의 "yield return" 기능을 사용 하는 것입니다. 위의 첫 번째 여섯 가지 규칙 검사는 단순히 문자열 속성에는 Dinner null 이거나 비워 둘 수 없습니다는 적용 합니다. 마지막 규칙은 좀 더 흥미 로우 며 호출을 추가할 수 있습니다이 프로젝트 확인에 ContactPhone PhoneValidator.IsValidNumber() 도우미 메서드에 숫자 형식 일치 Dinner의 국가입니다.

사용할 수 있습니다. 이 전화 유효성 검사 지원을 구현 하기 위해 NET의 정규식 지원 합니다. 다음은 간단한 PhoneValidator 구현을 추가할 수 있습니다는 국가별 Regex 패턴 검사를 추가할 수 있게 해 주는 프로젝트에:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a>유효성 검사 및 비즈니스 논리 위반 처리

위의 유효성 검사 및 비즈니스 규칙 코드 만들기 또는 업데이트를 저녁 식사를 하기 위해 노력 하 든 지 추가 된 했으므로 유효성 검사 논리 규칙 평가 하 고 적용 합니다.

개발자 예외를 발생 하지 않고에서 모든 위반의 목록을 검색 및 사전에 Dinner 개체가 유효한 지를 확인 하려면 아래와 같은 코드를 작성할 수 있습니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

잘못 된 상태에서를 저녁 식사를 저장 하려고 하는 경우는 DinnerRepository에서 save () 메서드를 호출할 때 예외가 발생 됩니다. Dinner의 변경 내용을 저장 하 고 Dinner 규칙 위반이 있는 경우 예외를 발생 시키려면 Dinner.OnValidate()에 코드를 추가한 전에 자동으로 LINQ to SQL Dinner.OnValidate() 부분 메서드 호출 하기 때문에 발생 합니다. 이 예외를 catch 하 고 대응적으로 문제를 해결 하려면 위반 목록을 검색할 수 있습니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

유효성 검사 및 비즈니스 규칙은이 모델 계층 내에서 및 UI 계층 내를 구현 되므로 이러한 적용 되며 응용 프로그램 내에서 모든 시나리오에서 사용 합니다. 수 나중에 변경 또는 비즈니스 규칙을 추가 하 고 Dinner 개체가 호환 인식 하는 모든 코드.

한 곳에서 비즈니스 규칙을 변경할 수 있는 유연성을가지고 있으므로, 이러한 변경 내용은 응용 프로그램 및 UI 논리, 전체에 걸쳐 ripple 필요 없이 잘 작성 된 응용 프로그램을 및 MVC 프레임 워크는 것이 좋습니다는 데 도움이 되는 혜택의 기호입니다.

### <a name="next-step"></a>다음 단계

이제 쿼리하고 데이터베이스 업데이트를 사용할 수 있는 모델에 답변이 있습니다.

이제 추가해보겠습니다 일부 컨트롤러와 뷰 주위에 HTML UI 환경을 빌드를 사용할 수 있는 프로젝트에.

> [!div class="step-by-step"]
> [이전](create-a-database.md)
> [다음](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
