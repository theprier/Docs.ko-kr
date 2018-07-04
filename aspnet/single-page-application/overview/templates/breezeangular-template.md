---
uid: single-page-application/overview/templates/breezeangular-template
title: Breeze/Angular 템플릿 | Microsoft Docs
author: madskristensen
description: Breeze/Angular 단일 페이지 응용 프로그램 템플릿
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/08/2013
ms.topic: article
ms.assetid: db31e909-563a-4516-aadd-62aa210ac7e4
ms.technology: ''
msc.legacyurl: /single-page-application/overview/templates/breezeangular-template
msc.type: authoredcontent
ms.openlocfilehash: 541d1a71b58a0d55651d823dc7425b7d1ce73cdb
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37378062"
---
<a name="breezeangular-template"></a>Breeze/Angular 템플릿
====================
[제작: Mads Kristensen](https://github.com/madskristensen)

> Breeze/Angular MVC 템플릿 Ward 벨에 의해 작성 되었습니다.
> 
> [Breeze/Angular MVC 템플릿 다운로드](https://go.microsoft.com/fwlink/?LinkId=286437)


[AngularJS](http://angularjs.org) 는 단일 페이지 응용 프로그램 (Spa) 빌드에 대 한 Google에서 오픈 소스 라이브러리입니다. 데이터 바인딩, 종속성 주입 및 화면 관리를 제공합니다. 와 함께 [BreezeJS](http://www.breezejs.com/?utm_source=ms-spa), 데이터 모델링 및 데이터 관리에 대 한 다른 오픈 소스 라이브러리가 훌륭한 HTML/JavaScript 클라이언트 앱을 위한 기본적인 구성 요소입니다.

Breeze/Angular SPA 템플릿 변형 켜져 합니다 [KnockoutJS SPA 템플릿](../introduction/knockoutjs-template.md) ASP.NET 및 Web Tools 2012.2 업데이트에 포함 합니다. Visual Studio 있다면 해야 예로 SPA를 실행 60 초 이내에 합니다.

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningTodoPage.png)

외부적으로, 응용 프로그램에서는 KnockoutJS SPA 템플릿 매우 유사 합니다. 하지만 내부적 상당히 다릅니다. KnockoutJS 템플릿 Knockout을 사용 하 여 데이터 바인딩 및 데이터 액세스에 대 한 원시 AJAX에 대 한 합니다. Breeze/Angular 템플릿 데이터 액세스에 대 한 데이터 바인딩 및 설치에 대 한 Angular를 사용합니다. 이러한 libaries 페이지 탐색 및 기록을 비롯 한 추가 기능을 사용 합니다.

응용 프로그램에 대 한 페이지는 다음과 같습니다.

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningAboutPage.png)

이 페이지는 현재 사용자 세션 중 실행 로그의 이벤트를 표시 합니다. 포함 하 여:

- 페이징 합니다. # 2와 # 7에서 Todo 컨트롤러 만들기를 note 합니다.
- 원격 쿼리 (3) 및 로컬 캐시 쿼리 (7).
- 새 저장 (5, 6) 및 (4) 엔터티를 수정 합니다.
- 유효성 검사 (#9), 클라이언트에서 변경 내용을 커밋하기 전에 사용자 실수를 수정할 수 있도록 데이터베이스에 변경 내용입니다.

이 템플릿에서 탐색을 더 포함:

- HTML 보기 템플릿의 동적으로 로드 합니다.
- Angular "지시문입니다."를 통해 사용자 지정 데이터 바인딩
- 모듈성 및 종속성 주입 합니다.
- 쿼리 필터, 정렬, 페이징, 프로젝션 및 관련된 엔터티를 포함 합니다.
- 여러 화면에 걸쳐 데이터를 공유 합니다.
- 단일 트랜잭션으로 여러 변경 내용을 저장 합니다.
- 유효성 검사 규칙을 JavaScript 클라이언트는 서버에서 자동으로 전파 합니다.

이제 시작해 보겠습니다.

## <a name="create-a-breezeangular-template-project"></a>Breeze/Angular 템플릿 프로젝트 만들기

다운로드 하 고 위의 다운로드 단추를 클릭 하 여 템플릿을 설치 합니다. 서식 파일은 Visual Studio 확장 (VSIX) 파일로 패키지 됩니다. Visual Studio를 다시 시작 해야 합니다.

에 **템플릿** 창 **설치 된 템플릿** 확장 하 고는 **Visual C#** 노드. 아래 **Visual C#** 를 선택 **웹**합니다. 프로젝트 템플릿 목록에서 선택 **ASP.NET MVC 4 웹 응용 프로그램**합니다. 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.

에 **새 프로젝트** 마법사 **Breeze Angular SPA**합니다.

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeNgSpaTemplate.png)

Ctrl-F5 키를 눌러 빌드하고 디버깅 하지 않고 응용 프로그램을 실행 또는 디버깅 실행 하려면 F5 키를 누릅니다.

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrLogin.png)

응용 프로그램을 처음 실행 하면 로그인 화면을 표시 합니다. "등록" 링크를 클릭 하 고 사용자 이름과 암호를 입력할 수 있는 보기에 새 페이지 glides 합니다. (로그인 및 등록 페이지 빌드됩니다 ASP.NET MVC를 사용 하 여.) 등록 양식을 제출 하면 계정에 대 한 두 개의 항목을 사용 하 여 TodoList 서버에 생성 합니다. 그런 다음 표시 하는 노란색에서.

![](http://www.breezejs.com/sites/all/images/spa-template/TodoList.png)

이제 사용자는 SPA land 있습니다. 모든 표시를 렌더링 되며 Knockout 및 쉽게 활용 하 여 클라이언트에서 관리 되는 todo 항목을 조작 하는 동안 발생 합니다. 사용자로 앱을 탐색 하는 중... 하지만 개발자의 눈 모양입니다. 브라우저에서 개발자 도구를 사용 하 여 네트워크 트래픽 캡처. (Internet Explorer에서: F12 키를 눌러 선택 합니다 **네트워크** 탭을 클릭 **캡처하기 시작할**.) 이제 다음과 같이 하십시오.

- 새 Todo 항목을 추가 합니다.
- 레이블을 클릭 하 고 Todo 항목 제목 편집
- 표시 항목 완료 하는 확인란을 선택 합니다. 제목을 편집할 수 없게 됩니다 있도록 textbox가 비활성화 되었는지 확인 합니다.
- 레이블의 오른쪽에 있는 'x'를 클릭 합니다. 항목 사라지고 데이터베이스에서 삭제 됩니다.
- 다른 항목을 선택 하 고 제목을 지웁니다. 제목은 필수 유효성 검사 오류를 받게 됩니다. 잠시 후에 이전 제목 복원 됩니다.
- 터무니 없이 긴 제목을 입력 합니다. 제목이 너무 깁니다 서로 다른 유효성 검사 오류를 받게 됩니다.
- "할 일 목록에 추가" 단추를 클릭 합니다. 왼쪽 위 목록에 새 목록이 표시 됩니다.
- TodoList 타이틀을 요구 하는 트리거 및 길이 유효성 검사를 사용 하 여 재생 합니다.
- 오류 메시지를 지우려면 제목 텍스트 상자를 클릭 합니다.
- TodoList 및 해당 todo 항목을 삭제 하려면 오른쪽 위 모서리에서 원에 있는 "x"를 클릭 합니다.
- 이러한 작업의 로그를 보려면 오른쪽 위에 있는 "정보" 링크를 클릭 합니다.

유효성 검사 논리는 간단 하 여 클라이언트 쪽 수행된. 서버 모델 클래스에 유효성 검사 특성은 클라이언트에 전파 하 고 클라이언트는 서버에 연결 하기 전에 자동으로 실행 합니다.

네트워크 트래픽을 검토 합니다. 설치 오류를 검색 하는 경우 서버에 대 한 호출 되었는지 확인 합니다. "/ Api/Todo/SaveChanges"로 POST 요청에 유효한 각 변경이 했습니다. Breeze 변경 내용을 번들 및 보내 함께 단일 요청으로 Web API 컨트롤러에 `SaveChanges` 메서드. PUT, POST 및 각 항목에 대 한 요청을 개별적으로 삭제 합니다. 그러면 KockoutJS SPA 템플릿에서 다릅니다.

또한 페이지에 대 한를 TodoList 사이 전환 하는 경우 네트워크 트래픽이 것을 볼 수 있습니다. 로컬 설치 캐시 하도록 제한 된 쿼리 때문입니다.

## <a name="peek-inside"></a>내 보기

이 응용 프로그램에는 클라이언트 쪽 및 서버 쪽에 있습니다. 클라이언트 쪽 스택 ("Scripts" 폴더에 있음)에서 타사 JavaScript 라이브러리와 조금 HTML 및 응용 프로그램 JavaScript 모듈 ("앱" 폴더에 있음)의 조합으로 구성 됩니다.

![](http://www.breezejs.com/sites/all/images/spa-template/NgClientArchitecture2.png)

UI 아키텍처 컨트롤러에서 지 원하는 프레젠테이션 코드에서 뷰의 HTML 위젯이 구분합니다. Angular 데이터 바인딩 시스템 각 지식이 없어도 다른 작업을 수행할 수 있도록 뷰 및 컨트롤러를 조정 합니다.

컨트롤러 요청 데이터 컨텍스트를 가져와서 모델 엔터티를 저장 합니다. 데이터 컨텍스트 Breeze JSON 쿼리 결과에서 자동 추적 모델 개체를 생성 하는 작업의 대부분을 위임 합니다.

서버 쪽 스택의 일부 개발자 코드 및 라이브러리로 구성 되며 세 가지 원칙.NET: Web API, Entity Framework 및 Breeze.NET:

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

기본 아키텍처 KockoutJS SPA 템플릿와 같습니다. 하지만 구현은 훨씬 더 간단: The Dto 삭제 및 Entity Framework 세부 정보를 대부분 Breeze.NET에 게 위임 된 합니다.

## <a name="next-steps"></a>다음 단계

여는 코드를 탐색 하는 것이 좋습니다 합니다 [광범위 한 토론](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa) 클라이언트와 서버 스택 손쉽게 웹 사이트의.

Breeze 클라이언트 쪽 쿼리를 다루기를 시도해 볼 수 있습니다. 일부 필터 및 정렬을 추가 합니다. 자세한 모델 속성과 엔드-투-엔드 SPA 개발을 위한 더 나은 이해할 수 있도록 더 많은 엔터티를 추가할 수 있습니다. 디자인의 확신할 경우 Todo 기능을 사용해 삭제 수 있으며 사용자 고유의로 교체할 수 있습니다.

즐거운 코딩을 경험하시기 바랍니다!
