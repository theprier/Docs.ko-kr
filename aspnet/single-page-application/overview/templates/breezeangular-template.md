---
uid: single-page-application/overview/templates/breezeangular-template
title: "간편/각 템플릿 | Microsoft Docs"
author: madskristensen
description: "간편/각 단일 페이지 응용 프로그램 템플릿"
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/08/2013
ms.topic: article
ms.assetid: db31e909-563a-4516-aadd-62aa210ac7e4
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /single-page-application/overview/templates/breezeangular-template
msc.type: authoredcontent
ms.openlocfilehash: faf28a510a83b7fa07585904344176601c2e1f34
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="breezeangular-template"></a>간편/각 서식 파일
====================
여 [Kristensen Mads](https://github.com/madskristensen)

> 간편/각 MVC 템플릿에서 워드 벨에 의해 작성 되었으므로
> 
> [간편/각도 MVC 템플릿 다운로드](https://go.microsoft.com/fwlink/?LinkId=286437)


[AngularJS](http://angularjs.org) 단일 페이지 응용 프로그램 (SPAs)는 Google에서 오픈 소스 라이브러리입니다. 데이터 바인딩, 종속성 주입 및 관리 화면을 제공합니다. 와 함께 사용할 [BreezeJS](http://www.breezejs.com/?utm_source=ms-spa), 데이터 모델링 및 데이터 관리에 대 한 다른 오픈 소스 라이브러리 뛰어난 HTML/JavaScript 클라이언트 앱에 대 한 필수 구성 요소가 있어야 합니다.

간편/각 SPA 서식 파일은 한 변형에는 [KnockoutJS SPA 템플릿](../introduction/knockoutjs-template.md) ASP.NET 및 Web Tools 2012.2 업데이트에 포함 합니다. Visual Studio 있다면 해야 SPA 예 실행 되 고 60 초 이내에 합니다.

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningTodoPage.png)

외부적으로, 응용 프로그램에서는 KnockoutJS SPA 템플릿에 매우 유사 합니다. 하지만 내부에서 매우 다릅니다. KnockoutJS 템플릿은 데이터 바인딩 및 데이터 액세스에 대 한 원시 AJAX Knockout를 사용합니다. 간편/각 템플릿은 데이터 액세스에 대 한 데이터 바인딩 및 옵션에 대 한 각을 사용합니다. 이러한 libaries 페이지 탐색 및 기록을 포함 하 여 추가 기능을 사용 하도록 설정 합니다.

응용 프로그램에 대 한 페이지는 다음과 같습니다.

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningAboutPage.png)

이 페이지는 현재 사용자 세션 동안 실행 로그의 이벤트를 표시 합니다. 포함 하 여:

- 페이징 합니다. Note # 2와 # 7에 Todo 컨트롤러 생성 합니다.
- 원격 쿼리 (3) 및 로컬 캐시 쿼리 (7).
- 새로 저장 (5, 6) (#4) 엔터티를 수정 합니다.
- 변경 내용을 데이터베이스에 변경 내용을 커밋하기 전에 사용자의 실수를 수정할 수 있으므로 (#9), 클라이언트에서 검증 합니다.

이 서식 파일에서 탐색을 자세히 포함 하 여:

- HTML 보기 템플릿 동적 로드 합니다.
- 각 "지시문"를 통해 사용자 지정 데이터 바인딩
- 모듈 및 종속성 주입 합니다.
- 쿼리 필터, 정렬, 페이징, 프로젝션 및 관련된 엔터티를 포함 합니다.
- 여러 화면에 걸쳐 데이터를 공유 합니다.
- 단일 트랜잭션으로 여러 변경 내용을 저장 합니다.
- 유효성 검사 규칙 JavaScript 클라이언트는 서버에서 자동으로 전파 합니다.

이제 시작해 보겠습니다.

## <a name="create-a-breezeangular-template-project"></a>간편/각도 템플릿 프로젝트 만들기

다운로드 하 고 위의 다운로드 단추를 클릭 하 여 서식 파일을 설치 합니다. 서식 파일은 확장 VSIX (Visual Studio) 파일로 패키지 됩니다. Visual Studio를 다시 시작 해야 합니다.

에 **템플릿** 창 선택 **설치 된 템플릿** 확장는 **Visual C#** 노드. 아래 **Visual C#**선택, **웹**합니다. 프로젝트 템플릿 목록에서 선택 **ASP.NET MVC 4 웹 응용 프로그램**합니다. 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.

에 **새 프로젝트** 선택 마법사 **간편 각도 SPA**합니다.

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeNgSpaTemplate.png)

빌드하고 디버깅 하지 않고 응용 프로그램을 실행 하려면 Ctrl + f 5를 누르거나 f5 키를 눌러 디버깅이 설정 된 상태로 실행 합니다.

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrLogin.png)

응용 프로그램을 처음 실행할 때 로그인 화면을 표시 합니다. 사용자 이름 및 암호를 입력할 수 있는 새 페이지를 glides 고 "등록" 링크를 클릭 합니다. (로그인 및 등록 페이지 빌드됩니다 ASP.NET MVC를 사용 하 여.) 등록 양식을 제출 하면 서버 계정에 대해 두 개의 항목과 TodoList를 생성 합니다. 그런 다음 표시에 노란색으로 설명 합니다.

![](http://www.breezejs.com/sites/all/images/spa-template/TodoList.png)

이제 SPA 토지 위치는입니다. 모든 항목을 보고 있습니다 Todos 조작 렌더링 되 고 서버의 Knockout 및 간편 도움을 사용 하 여 클라이언트에서 관리 하는 동안 발생 합니다. 응용 프로그램 사용자로 탐색 중... 하지만 개발자의 눈 합니다. 브라우저에서 개발자 도구를 사용 하 여 네트워크 트래픽을 캡처합니다. (Internet Explorer에서: F12 키를 눌러 선택 된 **네트워크** 탭을 클릭 **를 캡처하기 시작**.) 이제 다음과 같이 하세요.

- 새 할 일 항목을 추가 합니다.
- 레이블을 클릭 하 고 할 일 항목 제목을 편집합니다
- 완료 항목을 표시 하는 확인란을 선택 합니다. 공지는 textbox를 사용할 수 없으므로 제목을 편집할 수 없게 됩니다.
- 레이블의 오른쪽에 있는 'x'를 클릭 합니다. 항목 사라지고 데이터베이스에서 삭제 됩니다.
- 다른 항목을 선택 하 고 제목을 취소 합니다. 제목은 필요 유효성 검사 오류를 얻게 됩니다. 잠깐 일시 중지 된 후 이전 제목 복원 됩니다.
- 긴 터무니 없이 제목을 입력 합니다. 제목이 너무 깁니다 서로 다른 유효성 검사 오류를 얻게 됩니다.
- "할 일 목록 추가" 단추를 클릭 합니다. 왼쪽 위 목록에 표시 된 새 목록입니다.
- TodoList 제목, 필요한 트리거와 길이 유효성 검사를 재생 합니다.
- 오류 메시지의 선택을 취소 하 고 제목 입력란을 클릭 합니다.
- TodoList 및 해당 todos 삭제 하려면 오른쪽 위 모서리의 원 안에 있는 "x"를 클릭 합니다.
- 이러한 활동의 한 로그를 보려면 오른쪽 위에 있는 "정보" 링크를 클릭 합니다.

유효성 검사 논리는 간단 하 여 수행된 된 클라이언트입니다. 서버 모델 클래스에 유효성 검사 특성 클라이언트에 전파 하 고 클라이언트는 서버에 연결 하기 전에 자동으로 실행 됩니다.

네트워크 소통량을 검토 합니다. 옵션에 오류가 발생 하는 경우 서버에 대 한 호출 되었는지 확인 합니다. 각 올바른 변경 내용에 "/ api/Todo/SaveChanges" POST 요청에서 발생 했습니다. 옵션 변경 내용을 함께 묶는 하 고 보냅니다 함께 단일 요청으로 Web API 컨트롤러에 `SaveChanges` 메서드. PUT, POST 및 각 항목에 대 한 요청을 개별적으로 삭제를 낮추는 KockoutJS SPA 템플릿에서 차이가 있습니다.

또한는 TodoList 사이 및 페이지에 대 한 전환 하는 경우 네트워크 트래픽이 없음 것을 볼 수 있습니다. 쿼리 옵션의 로컬 캐시 제한 된 때문입니다.

## <a name="peek-inside"></a>내 보기

이 응용 프로그램에 클라이언트 쪽 및 서버 쪽 있습니다. 클라이언트 쪽 스택 ("Scripts" 폴더)에서 공급 업체 JavaScript 라이브러리와 약간 HTML과 응용 프로그램 JavaScript 모듈 ("app" 폴더에 있음)의 조합으로 구성 됩니다.

![](http://www.breezejs.com/sites/all/images/spa-template/NgClientArchitecture2.png)

UI 아키텍처 컨트롤러에서 지 원하는 프레젠테이션 코드에서 뷰의 HTML 위젯을 구분합니다. 각 데이터 바인딩 시스템과 각 작업은 다른 알지 못하면 작업을 수행할 수 있도록 뷰 및 컨트롤러를 조정 합니다.

컨트롤러에는 데이터 컨텍스트를 획득 하 고 모델 엔터티에 저장를 요청 합니다. 데이터 컨텍스트는 대부분의 JSON 쿼리 결과에서 자체 추적 모델 개체를 생성 하는 옵션을 작업을 위임 합니다.

서버 쪽 스택 일부 개발자 코드 및 세 가지 원칙.NET 라이브러리 구성: Web API, Entity Framework 및 Breeze.NET:

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

기본 아키텍처 KockoutJS SPA 템플릿으로 같습니다. 하지만 구현이 훨씬 더 간단: The Dto 삭제 된 및 Entity Framework의 대부분을 Breeze.NET에 게 위임 된 합니다.

## <a name="next-steps"></a>다음 단계

여는 코드를 확인 하는 것이 좋습니다는 [광범위 한 토론](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa) 클라이언트와 서버 스택 쉽게 웹 사이트에서의 합니다.

재생 옵션 클라이언트 쪽 쿼리로; 해 볼 수도 있습니다. 일부 필터 및 정렬을 추가 합니다. 더 많은 모델 속성 및 종단 간 SPA 개발을 위한 더 나은 이해할 수 있도록 더 많은 엔터티를 추가할 수 있습니다. 디자인의 확신할 경우 Todo 기능을 사용해 중지할 수 있으며 사용자의 정보로 바꾸세요.

즐거운 코딩을 경험하시기 바랍니다!
