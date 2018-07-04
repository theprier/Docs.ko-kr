---
uid: single-page-application/overview/introduction/other-libraries
title: Knockout 이외의 라이브러리를 알고 있습니까? | Microsoft 문서
author: madskristensen
description: Knockout 이외의 라이브러리를 알고 있습니까?
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/05/2013
ms.topic: article
ms.assetid: a8367c6d-ef94-4dff-a010-5eff9e6eea96
ms.technology: ''
msc.legacyurl: /single-page-application/overview/introduction/other-libraries
msc.type: authoredcontent
ms.openlocfilehash: 0424d209cbd24756d1a840788bb3dc5b48d905ff
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37375242"
---
<a name="know-a-library-other-than-knockout"></a>Knockout 이외의 라이브러리를 알고 있습니까?
====================
[제작: Mads Kristensen](https://github.com/madskristensen)

합니다 [단일 페이지 응용 프로그램 (SPA) 템플릿](knockoutjs-template.md) 단일 페이지 응용 프로그램 작성을 시작 하는 좋은 방법입니다. 템플릿을 사용 하 여 [KnockoutJS](http://knockoutjs.com/) DOM 요소를 응용 프로그램 데이터를 바인딩합니다.

하지만 Knockout 리치 클라이언트 응용 프로그램을 만들기 위한 유일한 JavaScript 라이브러리를 아닙니다. 다른 라이브러리 가지에서 유사한 문제를 해결 합니다. 변경한 여러 커뮤니티에서 만든 템플릿을 다운로드할 수 있으므로, 다른 하나의 라이브러리를 선호할 수 있습니다. 이러한 각 템플릿은 다양 한 클라이언트 JavaScript 라이브러리를 사용합니다.

커뮤니티에서 만든 서식 파일을 설치 하려면 페이지 아래에 나열 된 다운로드 단추를 클릭 하는 템플릿 중 하나를 방문 합니다. 템플릿을은 VSIX 파일로 제공 됩니다.

## <a name="backbonejs"></a>BackboneJS

[Backbone.js SPA 템플릿](../templates/backbonejs-template.md)합니다. 이 템플릿은 개발에 대 한 초기 스 켈 레 톤을 제공 합니다.는 [Backbone.js](http://backbonejs.org/) ASP.NET MVC 응용 프로그램입니다. 기본적으로 사용자 등록, 로그인, 암호 재설정 및 기본 전자 메일 템플릿 사용 하 여 사용자에 게 확인을 비롯 한 기본 사용자 로그인 기능을 제공 합니다.

## <a name="breezejs"></a>BreezeJS

[BreezeJS](http://www.breezejs.com/?utm_source=ms-spa) 는 JavaScript 클라이언트에서 다양 한 데이터를 관리 하기 위한 오픈 소스 라이브러리입니다. Breeze 쿼리, 캐싱, 변경 내용 추적, 유효성 검사 등을 처리 합니다. 두 템플릿 기능 설치:

- 합니다 [Breeze/Knockout](../templates/breezeknockout-template.md) 서식 파일은 단일 페이지 응용 프로그램을 쉽게 사용 하 여 데이터 관리 및 KnockoutJS 데이터 바인딩에 대 한 빌드 수는 얼마나 쉽게 보여 주는 Knockout SPA 템플릿을 확장 합니다.
- [Breeze/Angular](../templates/breezeangular-template.md) 서식 파일을 만들 수 있지만 사용 하 여 Knockout SPA 템플릿 확장을 [AngularJS](http://angularjs.org) 데이터 바인딩, 종속성 주입 및 화면 관리에 대 한 라이브러리입니다.

또한 합니다 [핫 수건 SPA 템플릿](../templates/hottowel-template.md) BreezeJS를 사용 합니다.

## <a name="emberjs"></a>EmberJS

[EmberJS SPA 템플릿](../templates/emberjs-template.md)합니다. 이 템플릿을 사용 하 여 [Ember](http://emberjs.com/), 다양 한 리치 클라이언트 응용 프로그램을 빌드하기 위한 문제를 해결 하는 강력한 MVC JavaScript 라이브러리입니다.

Ember와 SPA 템플릿 Handlebars 및 EmberJS 템플릿을 사용 하 여 Knockout SPA 템플릿 다시 구현 하는 경우

## <a name="hot-towel"></a>핫 수건

[핫 수건 SPA 템플릿](../templates/hottowel-template.md)합니다. 이 템플릿은 손쉽게, Knockout, RequireJS 및 Twitter Bootstrap을 비롯 한 여러 JavaScript 라이브러리에서 제공 합니다.

핫 수건 teample 여기에 나열 된 다른 템플릿을 사용 하 여 비교를 빌드할 수 있습니다 고유한 더 완전 한 응용 프로그램을 제공 합니다. 더 많은 개념을 알아야 할 있지만 이러한를 이해 하면이 템플릿을 사용자에 게 원하는 것입니다. 및 초에서 해야 모든 도구와 SPA SPA를 빌드하려면 싶지만 시작, 실행 부하 과다 수건을 사용 하 여 위치를 결정할 수 없는 경우에 작성 해야 합니다.

## <a name="feature-table"></a>기능 테이블

다음은 각 SPA 템플릿에서 제공 하는 기능입니다.


|                        | ASP.NET SPA | 백본 | Breeze/Angular | Breeze/KO |  Ember와   | 핫 수건 |
|------------------------|-------------|----------|----------------|-----------|----------|-----------|
|      할 일 샘플       |  &#10003;   |          |    &#10003;    | &#10003;  | &#10003; |           |
|     기본 템플릿      |             | &#10003; |                |           |          | &#10003;  |
| 탐색 및 기록 |             | &#10003; |    &#10003;    |           | &#10003; | &#10003;  |
|        Libaries        |             |          |                |           |          |           |
|        Angular         |             |          |    &#10003;    |           |          |           |
|    &#8195;백본     |             | &#10003; |                |           |          |           |
|         Breeze         |             |          |    &#10003;    | &#10003;  |          | &#10003;  |
|        durandal        |             |          |                |           |          | &#10003;  |
|         Ember와          |             |          |                |           | &#10003; |           |
|        Knockout        |  &#10003;   |          |                | &#10003;  |          | &#10003;  |

