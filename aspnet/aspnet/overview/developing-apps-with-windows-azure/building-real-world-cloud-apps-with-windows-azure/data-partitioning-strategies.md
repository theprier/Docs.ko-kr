---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
title: 데이터 분할 전략 (Azure로 응용 프로그램 빌딩 실제 클라우드) | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드로 응용 프로그램 빌딩 Azure 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴 및 그을 수 있는 방법에 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/12/2014
ms.topic: article
ms.assetid: 513837a7-cfea-4568-a4e9-1f5901245d24
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
msc.type: authoredcontent
ms.openlocfilehash: 9ff7f37a03d8d3dfab50e8007a6645bb0d88f453
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="data-partitioning-strategies-building-real-world-cloud-apps-with-azure"></a>데이터 분할 전략 (Azure로 응용 프로그램 빌딩 실제 클라우드)
====================
여 [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **실제 세계 클라우드로 응용 프로그램 빌딩 Azure** 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴에 설명 하 고 사례 수 있는 클라우드에 대 한 웹 앱을 개발 성공적으로 수행 되어야 합니다. 계열에 대 한 정보를 참조 하십시오. [첫 번째 장](introduction.md)합니다.


앞서 추가 하 고 웹 서버를 제거 하 여 클라우드 응용 프로그램의 웹 계층을 확장 하는 것이 얼마나 쉬운지에 대해 살펴보았습니다. 그러나은 모두 한 것 같은 데이터 저장소, 백 엔드에 프런트 이동 하는 응용 프로그램의 병목 현상이 가장 어려운 크기를 조정 하는 데이터 계층. 이 장에서 하도록 하는 방법 데이터 계층의 확장 가능한 여러 관계형 데이터베이스로 데이터를 분할 하 여 또는 다른 데이터 저장소 옵션으로 관계형 데이터베이스 저장소를 결합 하 여 살펴보겠습니다.

파티션 구성표를 설정 하는 것이 가장 좋습니다 앞에서 언급 한 이와 같은 이유로 든 완료: 응용 프로그램을 프로덕션 환경에서 다음 데이터 저장소 전략을 변경 하려면 매우 어렵습니다. 생각 되 면 하드 들겠지만 다양 한 접근 방법에 대 한, "Twitter 잠시" 응용 프로그램 충돌 또는 앱의 데이터 및 데이터 액세스 코드를 다시 구성 하는 동안 오랜 시간 동안 다운 될 경우를 방지할 수 있습니다.

## <a name="the-three-vs-of-data-storage"></a>데이터 저장소의 세 가지 Vs

분할 전략 및 것 필요한 지를 확인 하기 위해 데이터에 대 한 세 가지 질문을 고려 합니다.

- 볼륨 – 데이터의 양을 하나요 궁극적으로 저장 합니까? 몇 기가바이트? 몇 백 기가바이트? 테라바이트? 페타바이트?
- 개발 속도 – 데이터 늘어나는지 속도 얼마 입니까? 많은 데이터를 생성 하지 하는 내부 응용 프로그램 입니까? 외부 응용 프로그램을 이미지 및 비디오에 고객을 업로드 합니다.
- 다양 한 – 데이터는 입력을 저장 합니까? 관계형, 이미지, 키-값 쌍, 소셜 그래프?

볼륨, 속도 또는 다양 한 많은 하려는 경우 신중 하 게 파티션 구성표의 종류, 증가 속도 지연에 실행 하지 않는 되도록 및 효율적이 고 효과적으로 크기를 조정 하는 응용 프로그램에서는 가장을 고려해 야 합니다.

기본적으로 다음 3 가지 방법 분할과:

- 수직 분
- 행 분
- 혼합 분

## <a name="vertical-partitioning"></a>수직 분

같은 열으로 테이블을 분할은 세로 portioning: 하나의 열 집합을 하나의 데이터 저장소에 들어가고 다른 열 집합이 서로 다른 데이터 저장소로 이동 합니다.

예를 들어 이미지를 포함 하는 사람에 대 한 데이터를 저장 하는 응용 프로그램이 있다고 가정 합니다.

![데이터 표](data-partitioning-strategies/_static/image1.png)

표 형식으로이 데이터를 표시 하 고 다양 한 데이터를 확인 하는 경우 왼쪽에서 세 개의 열을 해당 c 저장 될 수 있는 효율적으로 관계형 데이터베이스에서 오른쪽에 두 개의 열은 기본적으로 바이트 배열을 문자열 데이터를 확인할 수 있습니다. 이미지 파일에서 홈입니다. 이미지 파일 데이터는 관계형 데이터베이스에 저장소 수 있으며 파일 시스템에 데이터를 저장 하려고 하지 않기 때문에 많은 사람들이 수행할 하 합니다. 필요한 양의 데이터를 저장할 수 있는 파일 시스템 없을 수 있습니다 또는 별도 백업 관리 하 고 시스템을 복원 하지 않을 수도 있습니다. 이 방법은 적은 양의 클라우드 데이터베이스의에서 데이터와 온-프레미스 데이터베이스에 대해 잘 작동합니다. 온-프레미스 환경에서 모든 것 DBA 자동 쉬울 수 있습니다.

하지만 클라우드 데이터베이스의 저장소는 상대적으로 비용이 많이 들며, 이미지의 대용량 하 게 되 고을 실행할 수 있는 효율적으로 한도 초과 하는 데이터베이스의 크기입니다. 데이터를 수직으로 분할 하 여 데이터의 테이블에 각 열에 대해 가장 적합 한 데이터 저장소를 선택 하는 것이 즉 이러한 문제 해결할 수 있습니다. 어떤 수에 가장 적합 한이 예제에서는 관계형 데이터베이스와 Blob 저장소에 있는 이미지에 문자열 데이터를 넣는 것입니다.

![수직 분할 데이터 테이블](data-partitioning-strategies/_static/image2.png)

데이터베이스 대신 Blob 저장소에 이미지를 저장 합니다.이 파일 서버를 설정 또는 백업 및 복원 하는 관계형 데이터베이스 외부에 저장 된 데이터 관리에 대해 걱정 하지 않아도 되므로 온-프레미스 환경에서 클라우드에서 더 효율적인: 모든 하는 처리 자동으로 Blob 저장소 서비스에 의해.

이 분할 하는 방법에 대 한 코드에서 살펴보게 및 수정 응용 프로그램에서 구현 했습니다는 [Blob 저장소 장](unstructured-blob-storage.md)합니다. 이 파티션 구성표 및 평균 이미지 크기는 3mb 가정 수정 앱만 됩니다 150 기가바이트의 최대 데이터베이스 크기에 도달 하기 전에 약 40000 작업을 저장할 수 있습니다. 이미지를 제거한 후 데이터베이스 10 배 이상 많은 작업을 저장할 수 있습니다. 가로 분할 체계를 구현 하는 방법에 대 한 신경쓸 필요가 전에 훨씬 더 오래를 이동할 수 있습니다. 않으며 매우 저렴 한 Blob 저장소로의 저장소 요구 사항 대량 들어가는 때문에 프로그램 비용에 따른 더 느리게 확장으로 응용 프로그램 크기를 조정 합니다.

## <a name="horizontal-partitioning-sharding"></a>행 분할 (분할)

테이블을 행으로 분할 비슷합니다 가로 portioning: 하나의 행 집합을 하나의 데이터 저장소에 들어가고 다른 행 집합이 서로 다른 데이터 저장소로 이동 합니다.

동일한 데이터 집합이 들어 또 다른 옵션 고객 이름에 서로 다른 범위를 다른 데이터베이스에에서 저장 하려는 것입니다.

![수평 분할 하는 데이터 테이블](data-partitioning-strategies/_static/image3.png)

핫 스폿을 방지 하기 위해 데이터가 고르게 배포 되 고 있는지 확인 하려면 분할 체계 때는 신중을 기해야 하려고 합니다. 성의 첫 문자를 사용 하 여이 간단한 예제 많은 사람들이 특정 일반적인 문자로 시작 하는 성이 때문에, 해당 요구 사항을 충족 하지 않습니다. 테이블 크기 제한을 대부분은 작은 상태로 유지 하는 동안 일부 데이터베이스 매우 큰 얻게 때문에 예상 보다 일찍 적중 합니다.

아래쪽 수평 분할이 데이터의 모든 쿼리를 위해이 어려울 수 있습니다. 이 예제에서는 응용 프로그램에서 저장 된 데이터를 모두 가져오려면 26 개 서로 다른 데이터베이스에서 가져올 쿼리 것입니다.

## <a name="hybrid-partitioning"></a>혼합 분

수직 및 수평 분할을 결합할 수 있습니다. 예를 들어 예제 데이터에서 이미지 Blob 저장소에 저장 및 문자열 데이터를 수평 분할 수 있습니다.

![데이터 테이블 하이브리드 분했습니다](data-partitioning-strategies/_static/image4.png)

## <a name="partitioning-a-production-application"></a>프로덕션 응용 프로그램을 분

개념적으로 쉽게 파티션 구성표를 작동 방식을 확인할 수는 있지만 모든 파티션 구성표 코드 복잡성이 증가 다룰 필요가 있는 많은 새 복잡성을 소개 합니다. 이미지를 blob 저장소를 이동할 경우 할까요 저장소 서비스가 다운 된 경우? Blob 보안 처리 하는 방법 데이터베이스 및 blob 저장소 동기화 되지 않을 경우 어떻게 됩니까? 분할 인 경우 어떻게 처리 하의 모든 데이터베이스 간 쿼리?

complication은으로 프로덕션 환경으로 전환 하기 전에을 계획 중인 관리할 수 있습니다. 그렇게 하지 않은 많은 사람들 나중에 사용 했던 선택 합니다. 평균 고객 자문 팀 (CAT) 팀 달에 한 번에 대 한 전화 통화 모르지만요 해당 응용 프로그램에서에서 수행 하는는 매우 큰 방식으로 고객 으로부터 가져오고이 계획을 수행 하지 않은 하 합니다. 이제 다음과 같이 및: "도움말! 단일 데이터 저장소에 모든 내용을 설정 하 고 45 일 이내에에 공간이 부족 합니다! " 및 데이터 저장소에 액세스 하는 방법에 기본 제공 되는 비즈니스 논리의 많은 경우 응용 프로그램을 사용 하는 고객을 있으면 시간은 없습니다 좋은 마이그레이션하는 동안 하루 아래로 이동 합니다. 통과 herculean 노력 고객 파티션 수 있도록 데이터 중단 시간 없이 즉석에서 얻게 됩니다. 매우 흥미롭고 매우 무시 무시 되며 하지 것에 포함 될 경우 원하는 방지할 수 있습니다! 들겠지만이 대해 생각 하 고 앱에 통합 하면 단순화 훨씬 더 쉽게 응용 프로그램 증가 하는 나중에 있습니다.

## <a name="summary"></a>요약

효과적인 파티션 구성표는 페타바이트 규모의 병목 현상 하지 않고도 클라우드에서 데이터를 확장 하는 클라우드 응용 프로그램에 사용 하도록 설정할 수 있습니다. 고 비용을 지불 들겠지만 대규모 컴퓨터 또는 광범위 한 인프라에 대 한 온-프레미스 데이터 센터에서 응용 프로그램을 실행 했을 수 있습니다 필요가 없습니다. 클라우드에서 할 수 있습니다 있습니다 필요한 만큼만 지불할 수를 사용 하는 만큼 자주 사용 하는 경우 그에 대 한 용량을 점진적으로 추가할 수 있습니다.

에 [다음 장에서](unstructured-blob-storage.md) 수정 응용 프로그램 이미지를 Blob 저장소에 저장 하 여 수직 분할 구현 하는 방법을 살펴보겠습니다.

## <a name="resources"></a>자료

분할 전략에 대 한 자세한 내용은 다음 리소스를 참조 합니다.

설명서:

- [Windows Azure 클라우드 서비스에서 대규모 서비스를 디자인에 대 한 유용한](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)합니다. 백서: Mark Simms 및 Michael Thomassy 합니다.
- [Microsoft Patterns and Practices-클라우드 디자인 패턴](https://msdn.microsoft.com/library/dn568099.aspx)합니다. 데이터 분할 지침, 분할 패턴을 참조 하세요.

비디오:

- [FailSafe: 복원 력 있는 확장 가능한 클라우드 서비스를 만드는](https://channel9.msdn.com/Series/FailSafe)합니다. Marc Mercuri, Ulrich Homann, Mark Simms 하 여 시리즈를 9 개 부분으로 구성 합니다. 고급 개념 및 아키텍처 원칙 매우 액세스 가능 하 고 흥미로운 방법으로 스토리 실제 고객과 Microsoft 고객 자문 팀 (CAT) 환경에서 가져온 것으로 표시 합니다. 분할 7 에피소드에서 참조 합니다.
- [건물 큰: 1 부에서 고객-Windows Azure에서에서 확인 된 사항을](https://channel9.msdn.com/Events/Build/2012/3-029)합니다. Mark Simms 파티션 구성 표, 분할 전략에 설명, 분할 및 19시 49분에서 시작 되는 SQL 데이터베이스 페더레이션을 구현 하는 방법입니다. 유사 Failsafe 시리즈 하지만 방법 더 세부적으로 이동 합니다.

샘플 코드:

- [클라우드 서비스 기본 사항 Windows Azure에서](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)합니다. 분할 된 데이터베이스를 포함 하는 샘플 응용 프로그램 구현 된 분할 체계에 대 한 참조 [DAL-RDBMS 분할](https://blogs.msdn.com/b/windowsazure/archive/2013/09/05/dal-sharding-of-rdbms.aspx) Windows Azure 블로그.

> [!div class="step-by-step"]
> [이전](data-storage-options.md)
> [다음](unstructured-blob-storage.md)
