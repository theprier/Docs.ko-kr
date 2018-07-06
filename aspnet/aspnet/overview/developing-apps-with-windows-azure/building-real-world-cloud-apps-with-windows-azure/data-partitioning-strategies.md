---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
title: 데이터 분할 전략 (실제 클라우드 앱 빌드 azure) | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드 앱 빌드 Azure 전자책을 사용 하 여 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴과 그을 수 있는 방법을 설명 하는 중...
ms.author: aspnetcontent
ms.date: 06/12/2014
ms.assetid: 513837a7-cfea-4568-a4e9-1f5901245d24
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
msc.type: authoredcontent
ms.openlocfilehash: 89921df4f84b86ef7c222f8e8c871f510856b4f3
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37819801"
---
<a name="data-partitioning-strategies-building-real-world-cloud-apps-with-azure"></a>데이터 분할 전략 (실제 클라우드 앱 빌드 Azure 사용 하 여)
====================
하 여 [Mike Wasson](https://github.com/MikeWasson)하십시오 [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 합니다 **실제 세계 클라우드 앱 빌드 Azure** 전자책 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴 설명 하 고 도움이 될 수 있는 사례 성공적인 클라우드를 위한 웹 앱을 개발할 수 있습니다. 시리즈에 대 한 자세한 내용은 [첫 번째 장에서](introduction.md)합니다.


이전에 추가 하 고 웹 서버를 제거 하 여 클라우드 응용 프로그램의 웹 계층의 크기를 얼마나 쉬운지 살펴보았습니다. 그러나 이러한 모든 발생 동일한 데이터 저장소, 응용 프로그램의 병목 상태에서 이동 프런트 엔드 백 엔드에 데이터 계층은 확장 하기 어렵습니다. 이 챕터에 만드는 방법을 데이터 계층의 확장 가능한 여러 관계형 데이터베이스로 데이터를 분할 하 여 또는 다른 데이터 저장소 옵션을 사용 하 여 관계형 데이터베이스 저장소를 결합 하 여 살펴봅니다.

파티션 구성표를 설정 하는 것이 가장 좋습니다 앞에서 언급 한 동일한 이유로 든 완료: 후 프로덕션 환경에서 앱이 데이터 저장소 전략을 변경 하기가 매우 어렵습니다. 생각해 보면 하드 인덱싱한 가지, "Twitter 잠시" 앱 작동이 중단 되거나 앱의 데이터 및 데이터 액세스 코드를 다시 구성 하는 동안 오랜 시간 동안 다운 되 면 것을 방지할 수 있습니다.

## <a name="the-three-vs-of-data-storage"></a>데이터 저장소의 세 가지 Vs

분할 전략 및 어떤 것이 필요한 지를 확인 하기 위해 데이터에 대 한 세 가지 질문을 고려 합니다.

- 볼륨-데이터의 양을 궁극적으로 저장 합니까? 몇 기가바이트? 몇 가지 백 기가바이트? 테라바이트? 페타바이트?
- – 속도는 데이터 증가 속도 얼마 입니까? 많은 양의 데이터를 생성 하지 않습니다 하는 내부 앱 입니까? 고객은 이미지 및 비디오를 업로드 해야 됩니다 하는 외부 앱?
- 다양 한 – 데이터의 형식을 저장 합니까? 관계형, 이미지, 키-값 쌍, 소셜 그래프?

볼륨, 속도 또는 다양 한 많은 하려는 경우 신중 하 게 파티션 구성표의 종류 앱 증가 속도 병목 상태를 실행 하지 않는 되도록 효율적으로 확장을 통해 가장을 고려해 야 합니다.

기본적으로 분할 하는 세 가지 방법

- 수직 분
- 가로 분
- 하이브리드 분

## <a name="vertical-partitioning"></a>수직 분

열을 기준으로 테이블을 분할 비슷합니다 세로 portioning: 열 집합이 하나 이상의 데이터 저장소에 들어가고 다른 열 집합을 다른 데이터 저장소로 이동 합니다.

예를 들어, 내 앱 이미지를 포함 하 여 사용자에 대 한 데이터를 저장 합니다.

![데이터 테이블](data-partitioning-strategies/_static/image1.png)

테이블로이 데이터를 나타내고 다양 한 데이터를 살펴볼 때 왼쪽에서 세 개의 열을 해당 c 오른쪽 두 열은 기본적으로 바이트 배열을 관계형 데이터베이스를 통해 효율적으로 저장할 수 있는 문자열 데이터가 있는지 확인할 수 있습니다. 이미지 파일에서 ome 합니다. 관계형 데이터베이스에서 이미지 파일 데이터를 저장소 이며 많은 사람들이 이렇게 파일 시스템에 데이터를 저장 하려고 하지 않기 때문입니다. 필요한 양의 데이터를 저장할 수 있는 파일 시스템 없을 또는 관리할 별도 백업 및 복원 시스템을 원하지 않을 수 있습니다. 이 방법은 적은 양의 클라우드 데이터베이스에서 데이터 및 온-프레미스 데이터베이스에 대 한 잘 작동합니다. 온-프레미스 환경에서 dba가 모든 것을 그대로 사용 하면 쉽게 수 있습니다.

하지만 클라우드 데이터베이스 저장소는 비교적 저렴 하 고 대용량 이미지의 증가는 작동할 수 효율적으로 제한을 초과 하는 데이터베이스의 크기를 만들 수 있습니다. 데이터를 수직으로 분할 하 여 데이터 테이블의 각 열에 대해 가장 적합 한 데이터 저장소를 선택 하는 것이 즉 이러한 문제 해결할 수 있습니다. 항목 수에 가장 적합 한이 예제에서는 관계형 데이터베이스 및 Blob storage에 이미지에서 문자열 데이터를 넣는 것입니다.

![수직 분할 하는 데이터 테이블](data-partitioning-strategies/_static/image2.png)

데이터베이스 대신 Blob storage에 이미지를 저장는 파일 서버를 설정 또는 백업 및 복원 외부 관계형 데이터베이스에서 저장 된 데이터의 관리에 대해 걱정할 필요가 없기 때문에 온-프레미스 환경에서 클라우드의 것이 좋습니다: 모든 처리 됩니다 자동으로 Blob 저장소 서비스에서.

이 방식은 분할 Fix It 응용 프로그램에서 구현에서는 및에 대 한 코드를 살펴보도록 하겠습니다 합니다 [Blob storage 장](unstructured-blob-storage.md)합니다. 이 파티션 구성표 및 3mb의 평균 이미지 크기를 가정 하지 않고 Fix It 앱만 수 150gb 최대 데이터베이스 크기에 도달 하기 전에 40,000 개의 작업을 저장 합니다. 데이터베이스 수 10 배의 작업을 저장 하는 데 이미지를 제거한 후 이동할 수 있습니다 훨씬 더 오래 전에 수평 분할 구성표를 구현 하는 방법에 대 한 고려해 야 합니다. 및 저장소 요구 사항을 대량은 매우 저렴 한 Blob 저장소로 이동 하기 때문에 비용에 더 느리게 증가 앱 확장으로 합니다.

## <a name="horizontal-partitioning-sharding"></a>행 분할 (분할)

행을 기준으로 테이블을 분할 비슷합니다 가로 portioning: 하나의 행 집합을 하나의 데이터 저장소로 이동 하 고 다른 행 집합이 서로 다른 데이터 저장소로 이동 합니다.

데이터 집합이 들어 또 다른 옵션 서로 다른 데이터베이스에 고객 이름 서로 다른 범위를 저장할 것입니다.

![수평 분할 하는 데이터 테이블](data-partitioning-strategies/_static/image3.png)

핫 스폿을 방지 하기 위해 데이터는 고르게 배포 되도록 분할 체계에 대 한 매우 주의 해야 합니다. 많은 사람들이 특정 일반 문자로 시작 하는 성이 없으므로 성의 첫 번째 문자를 사용 하 여이 간단한 예제에서 해당 요구 사항을 충족 하지 않습니다. 일부 데이터베이스는 매우 커질 대부분은 작게 유지 하는 동안 때문에 예상 보다 일찍 테이블 크기 제한에 도달할 것 있습니다.

아래쪽 변의 수평 분할 데이터의 모든 쿼리를 수행 하기가 수 없는 경우 이 예제에서는 그리기의 모든 앱에 저장 된 데이터를 가져오려는 26 개 다른 데이터베이스에서 쿼리를 해야 합니다.

## <a name="hybrid-partitioning"></a>하이브리드 분

수직 및 수평 분할을 결합할 수 있습니다. 예를 들어 예제 데이터에서 Blob 저장소에 이미지를 저장 및 문자열 데이터를 수평 분할 수 있습니다.

![데이터 테이블 하이브리드 분했습니다](data-partitioning-strategies/_static/image4.png)

## <a name="partitioning-a-production-application"></a>프로덕션 응용 프로그램 분

개념적으로 쉽게 파티션 구성표를 작동 하는 방법을 확인할 수 있지만 모든 파티션 구성표 코드 복잡성 증가 하 고 처리 해야 하는 많은 새 복잡성을 소개 합니다. 이미지를 blob 저장소로 이동 하는 경우 어떻게 해야 하나요 저장소 서비스가 종료 되 면? Blob 보안 처리 하는 방법 데이터베이스 및 blob storage는 동기화 되 면 어떻게 되나요? 분할 인 경우 어떻게 처리 하는 데이터베이스의 모든 쿼리?

복잡성을 감안 프로덕션으로 전환 하기 전에 해당 계획을 관리할 수 있는 합니다. 그렇게 하지 않은 많은 사람들이 나중에 가졌던 하려고 합니다. 평균 고객 자문 팀 (CAT) 팀 당황한 전화 달에 한 번에 대 한 해당 앱은 매우 큰 방식에서 사용량이 증가 하는 고객의 가져오고 계획 수행 되지 않았습니다. 같은 라고 말합니다. "도움말! 단일 데이터 저장소에 모든 항목을 넣었습니다 그리고 45 일 후에 가상 컴퓨터에 공간이 부족 합니다! " 되며 데이터 저장소에 액세스 하는 방법에 비즈니스 논리가 많이 있고 앱을 사용 하는 고객이 있는 경우 마이그레이션하는 동안 하루 작동이 없는 것이 좋습니다. 중단 시간 없이 즉석에서 해당 데이터를 고객 파티션 하는 데 herculean 노력을 통해 이동 얻게 됩니다. 활약 하 고 매우 두려운 및에 포함 될 원하는 것이 아닙니다 방지할 수 있습니다. 이 미리 생각 하 고 앱에 통합 됩니다 쉽게 훨씬 나중에 앱이 증가 하는 경우.

## <a name="summary"></a>요약

파티션 구성표를 적용 또는 페타바이트 단위의 병목 현상 없이 클라우드에서 데이터 크기를 조정 하 여 클라우드 앱을 설정할 수 있습니다. 및는 온-프레미스 데이터 센터에서 앱을 실행 하는 것 처럼 대규모 컴퓨터 또는 광범위 한 인프라에 대 한 미리 지불 필요가 없습니다. 클라우드에서 있습니다 필요 하 고 사용 하는 만큼 사용할 경우에 지불 하는 용량을 점진적으로 추가할 수 있습니다.

에 [다음 장에서](unstructured-blob-storage.md) Fix It 앱 Blob storage에 이미지를 저장 하 여 수직 분할을 구현 하는 방법을 살펴보겠습니다.

## <a name="resources"></a>자료

분할 전략에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

설명서:

- [Windows Azure Cloud Services에서 대규모 서비스 설계를 위한 모범 사례](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)합니다. Mark Simms 및 Michael Thomassy 백서입니다.
- [Microsoft Patterns and Practices-클라우드 디자인 패턴](https://msdn.microsoft.com/library/dn568099.aspx)합니다. 데이터 분할 지침, 분할 패턴을 참조 하세요.

비디오:

- [FailSafe: 복원 력 있는 확장 가능한 클라우드 서비스를 만드는 데](https://channel9.msdn.com/Series/FailSafe)합니다. Marc Mercuri, Ulrich Homann, Mark Simms에서 9 부 시리즈입니다. 고급 개념 및 아키텍처 원칙으로 실제 고객의 Microsoft 고객 자문 팀 (CAT) 환경에서 가져온 스토리를 사용 하 여 액세스 가능 하 고 흥미로운 방식으로 표시 합니다. 에피소드 7 분할 설명을 참조 하세요.
- [빌드 큰: Windows Azure 고객 부에서 Lessons learned](https://channel9.msdn.com/Events/Build/2012/3-029)합니다. 파티션 구성표, 분할 전략을 설명 하는 Mark Simms, 분할 및 SQL Database 페더레이션과 19시 49분부터 구현 하는 방법입니다. 비슷하지만 Failsafe 시리즈 자세한 방법 세부 정보로 이동 합니다.

샘플 코드:

- [클라우드 서비스 기본 사항 Windows Azure에서](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)합니다. 분할 된 데이터베이스를 포함 하는 샘플 응용 프로그램입니다. 구현 된 분할 체계에 대 한 참조 [DAL – 분할의 RDBMS](https://blogs.msdn.com/b/windowsazure/archive/2013/09/05/dal-sharding-of-rdbms.aspx) Windows Azure 블로그.

> [!div class="step-by-step"]
> [이전](data-storage-options.md)
> [다음](unstructured-blob-storage.md)
