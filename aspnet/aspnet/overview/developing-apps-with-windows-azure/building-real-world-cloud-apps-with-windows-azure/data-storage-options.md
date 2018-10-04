---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options
title: 데이터 저장소 옵션 (실제 클라우드 앱 빌드 azure) | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드 앱 빌드 Azure 전자책을 사용 하 여 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴과 그을 수 있는 방법을 설명 하는 중...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: e51fcecb-cb33-4f9e-8428-6d2b3d0fe1bf
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options
msc.type: authoredcontent
ms.openlocfilehash: 17e11c33d6bf2a75e99e3bda4d6ab89c5b1631f9
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577862"
---
<a name="data-storage-options-building-real-world-cloud-apps-with-azure"></a>데이터 저장소 옵션 (실제 클라우드 앱 빌드 Azure 사용 하 여)
====================
하 여 [Mike Wasson](https://github.com/MikeWasson)하십시오 [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 합니다 **실제 세계 클라우드 앱 빌드 Azure** 전자책 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴 설명 하 고 도움이 될 수 있는 사례 성공적인 클라우드를 위한 웹 앱을 개발할 수 있습니다. 전자책에 대 한 정보를 참조 하세요 [첫 번째 장에서](introduction.md)합니다.


클라우드 앱을 디자인 하는 경우 다른 데이터 저장소 옵션을 간과 하기가 및 대부분의 사람들은 관계형 데이터베이스에 사용 됩니다. 표시 될 수 있습니다, 더 나쁜 경우 최적 상태가 아닌 성능, 높은 비용 때문 [NoSQL](http://en.wikipedia.org/wiki/NoSQL) (비관계형) 데이터베이스는 몇 가지 작업을 관계형 데이터베이스 보다 더 효율적으로 처리할 수 있습니다. 고객에 게 중요 한 데이터 저장소 문제를 해결할 수 있도록 문의 경우에 종종 관계형 데이터베이스를 설정 하는 위치 NoSQL 옵션 중 하나 작동 했겠지만 향상이 있기 때문에 있습니다. 이러한 상황에서는 고객 좋았을 해제 프로덕션에 앱을 배포 하기 전에 NoSQL 솔루션을 구현 했습니다.

다른 한편으로 NoSQL 데이터베이스 수 있는 모든 작업 되거나 충분히 가정 만한 것입니다. 단일 최상의 데이터 관리 모든 데이터 저장소 작업에 대 한 다른 데이터 관리 솔루션은 다양 한 작업에 최적화 됩니다. 대부분의 실제 클라우드 앱 다양 한 데이터 저장소 요구 사항 및 여러 데이터 저장소 솔루션을 조합 하 여 가장 자주 제공 됩니다.

이 장의 목적은 클라우드 앱을 시나리오에 적합 한 속성을 선택 하는 방법에 대 한 몇 가지 기본 지침을 사용할 수 있는 데이터 저장소 옵션 보다 광범위 한 파악할 수 있도록 하는 것입니다. 응용 프로그램을 개발 하기 전에 해당 장점 및 단점에 대 한 생각 하 고 사용할 수 있는 옵션에 주의 해야 하는 것이 좋습니다. 프로덕션 앱에서 데이터 저장소 옵션을 변경 하는 평면 진행에서 중일 제트 엔진을 변경 하는 것과 매우 어려울 수 있습니다.

## <a name="data-storage-options-on-azure"></a>Azure에서 데이터 저장소 옵션

클라우드를 사용 하면 다양 한 관계형 및 NoSQL 데이터 저장소를 사용 하 여 비교적 쉽게입니다. Azure에서 사용할 수 있는 데이터 저장소 플랫폼의 다음과 같습니다.

![](data-storage-options/_static/image1.png)

다음 표에서 네 가지 유형의 NoSQL 데이터베이스를 보여줍니다.

- [키/값 데이터베이스](https://msdn.microsoft.com/library/dn313285.aspx#sec7) 각 키 값에 대 한 직렬화 된 단일 개체를 저장 합니다. 많은 양의 지정된 된 키 값에 대 한 하나의 항목을 가져오려는 없는 데이터를 저장 하기 위한 그렇다면 항목의 다른 속성을 기반으로 하는 쿼리.

    [Azure Blob storage](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/) 는 키/값 데이터베이스 폴더 및 파일 이름에 해당 하는 키 값을 사용 하 여 클라우드에서 파일 저장소와 같은 함수입니다. 파일 내용에서 값을 검색 하지, 해당 폴더와 파일 이름으로 파일을 검색할 수 있습니다.

    [Azure Table storage](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/) 키/값 데이터베이스 이기도 합니다. 각 값에 호출 되는 *엔터티* (파티션 키와 행 키로 식별 되는 행과 유사) 여러 개와 *속성* (열과 비슷하지만 있지만 테이블에서 모든 엔터티를 동일한 공유 해야 합니다. 열)입니다. 키 이외의 열에 대 한 쿼리는 매우 비효율적 및 피해 야 합니다. 예를 들어 단일 사용자에 대 한 정보를 저장 하는 파티션 하나를 사용 하 여 사용자 프로필 데이터를 저장할 수 있습니다. 동일한 파티션에 별도 엔터티 또는 한 엔터티의 별도 속성에 사용자 이름과 암호 해시, 생년월일 등와 같은 데이터를 저장할 수 있습니다. 생년월일의 지정된 된 범위를 사용 하 여 모든 사용자에 대 한 쿼리 하려고 하지만 사용자 프로필 테이블과 다른 테이블 간의 join 쿼리로 실행할 수 없습니다. Table storage는 확장성 및 관계형 데이터베이스 보다 저렴 하지만 복잡 한 쿼리 또는 조인을 사용 하지 않습니다.
- [Documentdatabases](https://msdn.microsoft.com/library/dn313285.aspx#sec8) 값이 있는 키/값 데이터베이스가 *문서*합니다. "Document" 여기 Word 또는 Excel 문서의 점에서 사용 되지 않습니다 하지만 명명 된 필드 및 하위 문서 수 있는 값의 컬렉션을 의미 합니다. 예를 들어, 주문 기록 테이블에는 주문 문서 있을 주문 번호, 주문 날짜 및 고객 필드 및 고객 필드 이름 및 주소 필드가 있을 수 있습니다. 데이터베이스는 XML, YAML, JSON 또는 BSON; 같은 형식으로 필드 데이터를 인코딩합니다. 또는 일반 텍스트를 사용할 수 있습니다. 키/값 데이터베이스 외에도 문서 데이터베이스를 설정 하는 기능 중 하나는 키가 아닌 필드에서 쿼리 및 보조 인덱스 보다 효율적으로 쿼리를 정의 하는 기능입니다. 이 기능을 사용 하면 문서 데이터베이스를 문서 키의 값 보다 더 복잡 한 조건에 따라 데이터를 검색 해야 하는 응용 프로그램에 더 적합 합니다. 예를 들어, 판매 주문 기록 문서 데이터베이스에서 제품 ID, 고객 ID, 고객 이름 등 다양 한 필드에서 쿼리할 수 있습니다. [MongoDB](http://www.mongodb.org/) 는 인기 있는 문서 데이터베이스입니다.
- [열 패밀리 데이터베이스](https://msdn.microsoft.com/library/dn313285.aspx#sec9) 는 키/값 데이터 저장소로 사용 하도록 설정 하면 구조를 데이터 저장소에 열 패밀리 라고 하는 관련 열의 컬렉션입니다. 예를 들어, 인구 조사 데이터베이스 하나의 개인의 이름에 대 한 열 그룹을 있을 (처음, 중간 이름, 성), 사용자의 주소에 대해 하나의 그룹 및 사용자의 프로필 정보 (DOB, 성별 등)에 대해 하나의 그룹입니다. 데이터베이스의 모든 키와 관련 된 동일한 두 명에 대 한 데이터를 유지 하면서 각 열 패밀리를 별도 파티션에 저장한 다음 수 있습니다. 그런 다음 모든 이름 및 주소 정보를 읽지 않고 모든 프로필 정보를 읽을 수 있습니다. [Cassandra](http://cassandra.apache.org/) 는 널리 사용 되는 열 패밀리 데이터베이스입니다.
- [그래프 데이터베이스](https://msdn.microsoft.com/library/dn313285.aspx#sec10) 개체 및 관계의 컬렉션으로 정보를 저장 합니다. 그래프 데이터베이스의 목적은 응용 프로그램을 서로 개체 및 관계의 네트워크를 트래버스하는 쿼리를 효율적으로 수행할 수 있도록 합니다. 예를 들어, 개체에는 인사 데이터베이스의 직원일 수 고를 용이 하 게 쿼리 같은 "find all employees who directly or indirectly work for Scott." [Neo4j](http://www.neo4j.org/) 는 인기 있는 그래프 데이터베이스입니다.

관계형 데이터베이스에 비해, NoSQL 옵션 훨씬 큰 확장성 및 구조화 되지 않은 데이터의 저장 및 분석에 대 한 비용 효율성을 제공 합니다. 단점은 풍부한 queryability 및 관계형 데이터베이스의 강력한 데이터 무결성 기능은 제공 하지 않습니다. NoSQL은 대용량 필요 없이 조인 쿼리를 포함 하는 IIS 로그 데이터에 대해 잘 작동 합니다. NoSQL가 작동 하지 않는 제대로 뱅킹 트랜잭션과, 절대 데이터 무결성 필요 하며 다른 계정 관련 데이터에 여러 관계가 포함 됩니다.

호출 하는 데이터베이스 플랫폼의 최신 범주 이기도 [NewSQL](http://en.wikipedia.org/wiki/NewSQL) queryability 및 관계형 데이터베이스의 트랜잭션 무결성을 사용 하 여 NoSQL 데이터베이스의 확장성을 결합 하는 합니다. NewSQL 데이터베이스는 분산된 저장소 및 쿼리 처리는 종종 "OldSQL" 데이터베이스에 구현 하기 위해 설계 되었습니다. [NuoDB](http://www.nuodb.com/) 은 Azure에서 사용할 수 있는 NewSQL 데이터베이스의 예입니다.

<a id="hadoop"></a>
## <a name="hadoop-and-mapreduce"></a>Hadoop과 MapReduce

NoSQL 데이터베이스에 저장할 수 있는 데이터의 대용량 적시에 효율적으로 분석할 어려울 수 있습니다. 같은 프레임 워크를 사용할 수 있는 작업을 수행 하 [Hadoop](http://hadoop.apache.org/) 구현 하는 [MapReduce](http://en.wikipedia.org/wiki/MapReduce) 기능입니다. 기본적으로 MapReduce 프로세스는 다음과 같습니다.

- 저장소 분석에 실제로 필요한 데이터만 데이터에서 선택 하 여 처리 해야 하는 데이터의의 크기 제한입니다. 예를 들어, 사용자 프로필 데이터 저장소에서 출생 연도 선택 하므로 출생 연도별로 기본 사용자의 구성을 확인 하려면.
- 부분으로 데이터를 세분화 하 고 처리를 위해 다른 컴퓨터로 전송할 합니다. 1950 1959 날짜를 사용 하 여 사용자의 수를 계산 하는 컴퓨터, 컴퓨터 B에 1960-1969, 등입니다. 이 컴퓨터 그룹은 호출 되는 *Hadoop 클러스터*합니다.
- 부분에 처리가 완료 된 후 각 파트의 결과 다시 배치 합니다. 이제 비교적 짧은 목록이 각 출생 연도 대해 얼마나 많은 사용자 및이 전체 목록에는 백분율을 계산 하는 작업은 관리 합니다.

Azure에서 [HDInsight](https://azure.microsoft.com/services/hdinsight/) 처리, 분석 및 Hadoop의 기능을 사용 하 여 빅 데이터에서 새로운 통찰력을 얻을 수 있습니다. 예를 들어, 웹 서버 로그 분석을 사용할 수 있습니다.

- 저장소 계정에 웹 서버 로깅을 사용 하도록 설정 합니다. 이 응용 프로그램에 모든 HTTP 요청에 대 한 Blob Service에 로그를 쓸 Azure를 설정 합니다. Blob Service는 기본적으로 클라우드 파일 저장소 및 HDInsight를 사용 하 여 원활 하 게 통합 됩니다. 

    ![Blob Storage에 로그](data-storage-options/_static/image2.png)
- 앱 트래픽을 가져옵니다, 웹 서버 IIS 로그 Blob 저장소에 작성 됩니다. 

    ![웹 서버 로그](data-storage-options/_static/image3.png)
- 포털에서 클릭 **새로 만들기** - **Data Services** - **HDInsight** - **빨리 만들기**, 고는 HDInsight 클러스터 이름, 클러스터 크기 (HDInsight 클러스터 데이터 노드 수) 및 사용자 이름 및 HDInsight 클러스터에 대 한 암호를 지정 합니다. 

    ![HDInsight](data-storage-options/_static/image4.png)

이제 MapReduce 작업을 로그를 분석 하 고 같은 질문에 답변을 받을 수를 설정할 수 있습니다.

- 하루 중 시간에 내 앱 가져오기 최대 또는 최소 트래픽
- 어떤 국가에서 들어오는 트래픽과 인가요?
- 제공 되는 트래픽과 영역의 평균 환경 소득입니다. (IP 주소, 환경 income을 제공 하는 공용 데이터 집합을 되며 웹 서버 로그에서 IP 주소에 대해 일치 수 있습니다.)
- 특정 페이지 또는 사이트에서 제품 환경 income 연결 하는 방법

그런 다음 고객에 게 가능성에 따라 또는 특정 제품을 구입할 가능성이 높은 대상 광고에 이와 같은 질문에 대 한 답변을 사용할 수 있습니다.

에 설명 된 대로 합니다 [장 모든 자동화](automate-everything.md), 포털에서 수행할 수 있는 대부분의 함수를 자동화 하 고 설정 하 고 HDInsight 분석 작업을 실행 하는 포함 되어 있습니다. 일반적인 HDInsight 스크립트는 다음 단계를 포함할 수 있습니다.

- HDInsight 클러스터를 프로 비전 하 고 Blob storage 입력에 대 한 저장소 계정에 연결 합니다.
- HDInsight 클러스터에 MapReduce 작업 실행 파일 (.exe 또는.jar 파일)을 업로드 합니다.
- Blob storage에 출력 데이터를 저장 하는 MapReduce를 제출 합니다.
- 작업이 완료 될 때까지 기다립니다.
- HDInsight 클러스터를 삭제 합니다.
- Blob 저장소에서 출력에 액세스 합니다.

이 모든 작업을 수행 하는 스크립트를 실행 하 여 비용을 최소화 하는 HDInsight 클러스터 프로 비전 되는 시간의 양을 최소화할 수 있습니다.

<a id="paasiaas"></a>
## <a name="platform-as-a-service-paas-versus-infrastructure-as-a-service-iaas"></a>Platform-as-a-service (PaaS) 인프라 및 서비스 (IaaS)

앞에 나열 된 데이터 저장소 옵션에는 플랫폼-as a Service (PaaS) 및 인프라-as a Service (IaaS) 솔루션을 모두 포함 됩니다. PaaS는 하드웨어 및 소프트웨어 인프라를 관리 하는 것만 서비스를 사용 하면 있음을 의미 합니다. SQL Database에는 Azure의 PaaS 기능입니다. 데이터베이스에 대 한 요청 하 고 백그라운드에서 Azure 설정 및 Vm을 구성 하 고 에서도 데이터베이스를 설정 합니다. Vm에 직접 액세스할 수 없는 관리할 필요가 없습니다. IaaS에서 원하는 항목을 추가한 설정, 구성 및 관리는 데이터 센터 인프라에서 실행 되는 Vm을 의미 합니다. 일반 VM 구성에 대 한 미리 구성 된 VM 이미지 갤러리에 제공합니다. 예를 들어, Windows Server 2008, Windows Server 2012, BizTalk Server, Oracle WebLogic Server, Oracle 데이터베이스 등 실행 하는 것에 대 한 미리 구성 된 VM 이미지를 설치할 수 있습니다.

Azure에서 제공 하는 PaaS 데이터 솔루션은 다음과 같습니다.

- Azure SQL Database (이전의 SQL Azure)입니다. SQL Server를 기반으로 관계형 클라우드 데이터베이스입니다.
- Azure 테이블 저장소입니다. 키/값 NoSQL 데이터베이스입니다.
- Azure Blob 저장소입니다. 클라우드에서 파일 저장소입니다.

IaaS에 대 한 예를 들어 vm을 로드할 수 있습니다 하는 아무 것도 실행할 수 있습니다.

- SQL Server, Oracle, MySQL, SQL Compact, SQLite 또는 Postgres와 같은 관계형 데이터베이스입니다.
- Riak Memcached, Redis, Cassandra 등 키/값 데이터를 저장합니다.
- HBase와 같은 열 데이터를 저장합니다.
- MongoDB, RavenDB, CouchDB 등 문서 데이터베이스입니다.
- Neo4j 등 그래프 데이터베이스입니다.

![Azure에서 데이터 저장소 옵션](data-storage-options/_static/image5.png)

IaaS 옵션을 사용 하면 거의 무제한 데이터 저장소 옵션 및 그 중 대부분은 미리 구성 된 이미지를 사용 하 여 Vm을 만들 수 있으므로 특히 쉽게 사용할 수 있습니다. 예를 들어, 관리 포털에서로 이동 **Virtual Machines**를 클릭 합니다 **이미지** 탭을 클릭 **VM Depot 찾아보기를**합니다.

![VM Depot 찾아보기](data-storage-options/_static/image6.png)

목록을 표시 [수백 개의 미리 구성 된 VM 이미지](http://www.hanselman.com/blog/Over400VirtualMachineImagesOfOpenSourceSoftwareStacksInTheVMDepotAzureGallery.aspx), MongoDB, 등 Neo4J, Redis, Cassandra, CouchDB, 사전 설치 하는 데이터베이스 관리 시스템에 있는 이미지에서 VM을 만들 수 있습니다.

![VM Depot에서 MongoDB](data-storage-options/_static/image7.png)

Azure에서는 IaaS 데이터 저장소 옵션을 최대한 사용 하기 쉬운 했지만 PaaS 제품 수 있게 해 주는 다양 한 시나리오에 대 한 실용적인 비용 효율적 이며 많은 이점:

- Vm을 만들 필요가 없습니다만 데이터 저장소를 설정 하려면 스크립트나 포털을 사용 합니다. 200 테라바이트 데이터 저장소를 원한다 면 방금 단추를 클릭 하거나 명령을 실행할 수 및 시간 (초)에서 사용할 준비가 완료 된 것입니다.
- 관리 하거나 서비스에서 사용 하는 Vm을 패치할 필요가 없습니다. Microsoft는이를 자동으로 합니다.-인프라 크기 조정 또는 높은 가용성;에 대 한 설정에 대해 걱정할 필요가 없습니다 Microsoft는 수에 대 한 모든 처리합니다.
- 라이선스를 구입 하지 않아도 됩니다. 라이선스 요금과 서비스 요금에 포함 됩니다.
- 사용한 만큼만 지불 합니다.

Azure에서 PaaS 데이터 저장소 옵션에는 타사 공급자가 제공 포함 됩니다. 예를 들어, 선택할 수 있습니다 합니다 [MongoLab 추가 기능](https://azure.microsoft.com/documentation/articles/store-mongolab-web-sites-dotnet-store-data-mongodb/) 서비스로 MongoDB 데이터베이스를 프로 비전 할 Azure Store에서.

## <a name="choosing-a-data-storage-option"></a>데이터 저장소 옵션을 선택합니다.

모든 시나리오에 적합 한 가지 방법은 없습니다. 누구나이 기술은 답변 됨 인 경우 먼저 요청 이므로 "란 질문?", 다른 솔루션은 다른 작업에 최적화 된 합니다. 이점이 한정 된 관계형 모델 때문에 따라서 오랫동안 해결 되었습니다. 하지만 NoSQL 솔루션을 사용 하 여 해결할 수 있는 sql 아래쪽 면도 있습니다.

종종 보이는 최선의 작업은 구성 방법에서에서 사용 하는 SQL 및 NoSQL 단일 솔루션입니다. 도 때 사람들의 이야기는 수용 하는 NoSQL 어떤 수행 중인 있습니다 종종를 드릴 하는 경우 몇 가지 다른 NoSQL 프레임 워크를 사용 하는 찾기: 사용 하 든 [CouchDB](http://wiki.apache.org/couchdb/Introduction), 및 [Redis](http://redis.io/), 및 [ Riak](http://basho.com/riak/) 다른 항목에 대 한 합니다. 도 Facebook, NoSQL을 광범위 하 게 사용 하는 서비스의 다른 부분에 대 한 다른 NoSQL 프레임 워크를 사용 합니다. 데이터 저장소 방법을 조합 하는 유연성의 여러 데이터 솔루션을 사용 하 고 단일 앱에 통합할 수 있기 때문에 클라우드에 대 한 훌륭한 것 중 하나입니다.

몇 가지 질문 접근 방식을 선택 하는 경우에 대해 생각 하는 다음과 같습니다.

| 의미 체계 데이터 | -의미 체계 핵심 데이터 저장소 및 데이터 액세스 새로운 기능 (사용자 데이터를 저장할 관계형 또는 구조화 되지 않은)? Blob storage에 가장 적합 한 미디어 파일과 같은 구조화 되지 않은 데이터 제품, 인벤토리, 공급 업체, 고객 주문 등과 같은 관련 된 데이터의 컬렉션에는 관계형 데이터베이스에 가장 적합 한 합니다. |
| --- | --- |
| 쿼리 지원 | -얼마나 쉬운지는 데이터를 쿼리할 수 있습니까? -형식의 질문 수 있는 효율적으로 요청? 키/값 데이터 저장소 키 값을 지정 된 단일 행에 매우 좋은 복잡 한 쿼리에 대해 그렇게 좋지 없습니다. 사용자 프로필 데이터 저장소는 항상 발생 하는 하나의 특정 사용자에 대 한 데이터에 대 한 키/값 데이터 저장소 수 제대로 작동 합니다. 다양 한 제품 특성을 기반으로 하는 다른 그룹 가져오려는 제품 카탈로그에 대 한 관계형 데이터베이스는 더 적합할 수 있습니다. NoSQL 데이터베이스는 효율적으로 볼륨이 큰 데이터를 저장할 수 있고 앱에서 데이터를 쿼리 하는 방법을 중심 데이터베이스를 구성 해야이 어려워집니다 임시 쿼리 작업을 수행 하 합니다. 관계형 데이터베이스를 사용 하 여 거의 모든 종류의 쿼리를 빌드할 수 있습니다. |
| 프로젝션 기능 | -질문 수, 집계 등 실행된 한 서버 쪽? SELECT COUNT를 실행 하면 (\*) sql에서 테이블에서 매우 효율적으로 서버에서 모든 작업을 수행 하 고 숫자를 찾고 반환 합니다. 집계를 지원 하지 않는 NoSQL 데이터 저장소에서 동일한 계산을 원한다 면 비효율적인 "바인딩되지 않은 쿼리를" 이며 아마도 시간이 초과 됩니다. 쿼리가 성공 하는 경우에 해야 클라이언트에 서버에서 모든 데이터 검색 및 클라이언트에 행을 계산 합니다. -어떤 언어 또는 식의 형식으로 사용할 수 있습니다? SQL 관계형 데이터베이스를 사용 하 여 사용할 수 있습니다. Azure Table storage와 같은 일부 NoSQL 데이터베이스를 사용 하 여 사용할 수 [OData](http://www.odata.org/), 기본 키에서 필터링 하 고 (사용 가능한 필드의 하위 집합을 선택 합니다.)를 예상를 이며 모두 수행할 수 있습니다. |
| 확장의 용이성 | -간격과 크기는 데이터 크기를 조정 해야? -스케일 아웃은 플랫폼에서 고유 하 게 구현 하지? -하기가 쉽습니까 용량 (크기 및 처리량)를 추가/제거 하 시겠습니까? 관계형 데이터베이스 및 테이블 되지 확장 제한이 초과 하기 어려운 되므로 확장성 있도록 자동으로 분할 합니다. Azure Table storage와 같은 NoSQL 데이터 저장소에 모든 항목을 기본적으로 분할 하 고 파티션을 추가에 대 한 제한은 거의 없습니다. 200 테라바이트 테이블 저장소를 쉽게 확장할 수 있습니다 하지만 Azure SQL Database에 대 한 최대 데이터베이스 크기는 500 기가바이트입니다. 여러 데이터베이스로 분할 하 여 관계형 데이터를 확장할 수 있습니다 하지만 프로그래밍 작업이 많은 수행 해야 해당 모델을 지 원하는 응용 프로그램을 설정 합니다. |
| 계측 및 관리 효율성 | -얼마나 쉬운지 계측, 모니터링 및 관리 하는 플랫폼이 있습니까? 플랫폼을 무료로 제공 하는 메트릭은 무엇을 알아야 할 되므로 데이터 저장소의 성능과 상태에 대 한 유지 해야 및 직접 개발 해야 합니다. |
| 작업 | -Azure에서 배포 및 실행 하는 플랫폼 얼마나 쉬운지 기능 PaaS? IaaS? Linux? Table Storage 및 SQL Database는 쉽게 Azure에서 설정할 수 있습니다. Azure PaaS 솔루션을 기본 제공 되지 않는 플랫폼에는 더 많은 노력이 필요 합니다. |
| API 지원 | -쉽게 플랫폼을 사용 하는 API 사용 가능한가? Azure Table Service에 대 한 SDK는.NET 4.5의 비동기 프로그래밍 모델을 지 원하는.NET API를 사용 하 여 있습니다. .NET 앱을 작성 하는 경우 쉽게 작성 하 고 API가 없습니다. 또는 덜 포괄적 있는 다른 키/값 열 데이터 저장소 플랫폼에 비해 Azure Table Service에 대 한 코드를 테스트할 수 있습니다. |
| 트랜잭션 무결성 및 데이터 일관성 | -는 중요 한 데이터 일관성을 보장 하기 위해 플랫폼 트랜잭션을 지원는 무엇입니까? 대량 전자 메일 전송, 성능 및 낮은 데이터 저장소 비용 트랜잭션이나 데이터 플랫폼에서 참조 무결성에 대 한 자동 지원 보다 더 중요할 수는 추적에 대 한 Azure Table Service를 적합 한 수행 합니다. 은행 계좌를 추적 하기 위한 분산 또는 구매 주문서 강력한 트랜잭션 보장에 더 적합할 것을 제공 하는 관계형 데이터베이스 플랫폼입니다. |
| 비즈니스 연속성 | -백업, 복원 및 재해 복구 얼마나 쉬운지 인가요? 프로덕션 데이터는 손상 조만간 및 함수를 실행 취소 해야 합니다. 관계형 데이터베이스에는 지점으로 복원 하는 기능과 같은 더 많은 세분화 된 복원 기능 있는 경우가 많습니다. 고려해 야 할 중요 한 요소는 여러분이 고려 하는 각 플랫폼에서 사용할 수 있는 복원 기능을 이해 합니다. |
| 비용 | -둘 이상의 플랫폼 데이터 워크 로드에서 지원할 수 있는 경우 어떻게 비교할 수 비용이 있습니까? 예를 들어 ASP.NET Id를 사용 하면 Azure Table Service 또는 Azure SQL Database에 사용자 프로필 데이터를 저장할 수 있습니다. SQL Database의 기능을 쿼리 하는 풍부한 필요가 없는 경우 선택할 수 있습니다 Azure 테이블에 많은 비용 때문에 지정 된 크기의 저장소가 이하인 합니다. |

일반적으로 권장 사항 데이터 저장소 솔루션을 선택 하기 전에 이러한 각 범주에 있는 질문에 대 한 답을 것입니다.

또한 워크 로드 일부 플랫폼에서 다른 항목 보다 더 잘 지원할 수 있는 특정 요구 사항이 있을 수 있습니다. 예를 들어:

- 감사 기능을 응용 프로그램에 필요한 사용자는?
- 데이터 수명 요구 사항은 무엇입니까-자동화 된 보관 또는 제거 기능이 필요 한가요?
- 특수 한 보안 요구 사항 있습니까? 예를 들어 데이터 PII (개인 식별이 가능한 정보)를 포함 하지만 해당 PII는 쿼리 결과에서 제외 해야 할 수 해야 합니다.
- 일부 데이터 규정 또는 기술적 이유로 클라우드에 저장할 수 없는 경우 온-프레미스 저장소를 사용 하 여 통합을 용이 하 게 하는 클라우드 데이터 저장소 플랫폼을 해야 할 수 있습니다.

## <a name="demo--using-sql-database-in-azure"></a>데모 – SQL Database를 사용 하 여 Azure에서

Fix It 응용 프로그램 작업을 저장 하는 관계형 데이터베이스를 사용 합니다. 에 표시 된 환경 만들기 Windows PowerShell 스크립트를 [장 모든 자동화](automate-everything.md) 두 SQL Database 인스턴스를 만듭니다. 포털에서 이러한 클릭 하 여 볼 수 있습니다 합니다 **SQL Database** 탭 합니다.

![포털에서 SQL 데이터베이스](data-storage-options/_static/image8.png)

포털을 사용 하 여 데이터베이스를 만들기도 쉽습니다.

클릭 **새로 만들기-Data Services** -- **SQL Database** -- **빨리 만들기**데이터베이스 이름, 계정에 이미 있는 서버를 선택 합니다. 또는 새 대시보드를 만들고 클릭 **SQL 데이터베이스 만들기**합니다.

![새 SQL Database](data-storage-options/_static/image9.png)

몇 초 정도 기다린 후 데이터베이스를 사용 하 여 준비 하는 Azure에서 만든.

![만든 새 SQL Database](data-storage-options/_static/image10.png)

Azure는 몇에서 시간 (초) 어떤 필요할 수 있습니다 하루 하므로 주 또는 온-프레미스 환경에서 수행 하는 데 더 합니다. 스크립트에서 또는 관리 API를 사용 하 여 자동으로 데이터베이스를 작성할 수 손쉽게를 확장할 수 있습니다 동적으로 여러 < 된 > 데이터베이스에 데이터를 분산 하 여 응용 프로그램에 대 한 프로그래밍 되었습니다 하기만 하 고 있습니다. < /o : p >

이것이 우리의 플랫폼-as a Service 모델의 예입니다. 서버를 관리할 필요가 없습니다, 그리고 것입니다. 백업에 걱정할 필요가 없습니다, 그리고 것입니다. 고가용성-에서 실행 중인 데이터베이스의 데이터를 자동으로 세 명의 서버에 걸쳐 복제 됩니다. 소멸 되는 컴퓨터에서는 자동으로 장애 조치 하 고 데이터가 손실 됩니다. 서버는 정기적으로 패치를 신경 쓸 필요가 없습니다.

단추를 클릭 하 고 필요 하 고 새 데이터베이스를 사용 하 여 바로 시작할 수 있습니다 정확 하 게 연결 문자열을 가져옵니다.

![연결 문자열](data-storage-options/_static/image11.png)

대시보드에 사용 되는 저장소의 양과 연결 기록을 보여 줍니다.

![SQL Database 대시보드](data-storage-options/_static/image12.png)

포털에서 데이터베이스를 관리할 수 있습니다이 든 SQL Server 도구를 사용 하 여 이미 익숙한 SQL Server Management Studio (SSMS) 및 Visual Studio 도구 서버 탐색기 및 SQL Server 개체 탐색기 (SSOX)를 포함 합니다.

![SSOX](data-storage-options/_static/image13.png)

또 다른 좋은 점은 가격 책정 모델입니다. 20MB 무료 데이터베이스를 사용 하 여 개발을 시작할 수 있습니다 하 고 프로덕션 데이터베이스에 대 한 5 달러 / 월에서 시작 합니다. 최대 용량 하지 데이터베이스에 실제로 저장 하는 데이터의 양에 대만 지불 하면 됩니다. 라이선스를 구입할 필요가 없습니다.

SQL Database는 쉽게 확장 됩니다. Fix It 응용 프로그램에 대 한 자동화 스크립트에서 만드는 데이터베이스 1 자리로 제한 됩니다. 150 기가 최대 크기를 조정 하려는 경우 방금 포털로 이동 하 고 해당 설정을 변경 하거나 REST API 명령을 실행 (초)에서 수 있으며 데이터를 배포할 수 있는 150 기가 데이터베이스 있습니다.

![SQL Database 버전 및 크기](data-storage-options/_static/image14.png)

강력한 인프라를 빠르고 쉽게 구축 하 고 즉시 사용을 시작 하려면 클라우드입니다.

Fix It 앱은 두 개의 SQL 데이터베이스, 멤버 자격 (인증 및 권한 부여)에 대 한 하나 및 데이터에 대 한 하나 이며이 프로 비전 및 크기를 조정 하기 위해 수행 해야 합니다. 앞서 살펴본 것이 얼마나 쉬운지는 포털에서 작업을 수행 하도 살펴보았습니다 및 Windows PowerShell 스크립트를 통해 데이터베이스를 프로 비전 하는 방법입니다.

## <a name="entity-framework-versus-direct-database-access-using-adonet"></a>ADO.NET를 사용 하 여 데이터베이스를 직접 액세스와 엔터티 프레임 워크

Entity Framework를 사용 하 여 이러한 데이터베이스를 액세스 하는 Fix It 응용 프로그램, Microsoft의.NET 응용 프로그램에 대 한 ORM (개체 관계형 매퍼)를 권장 합니다. ORM 개발자 생산성을 용이 하 게 하는 효과적인 도구 이지만 몇 가지 시나리오에서 성능 저하의 대가로 생산성 합니다. 실제 클라우드 앱에서 EF를 사용 하거나 직접 ADO.NET을 사용 하 여 선택할 수행 되지 않습니다-모두 사용 합니다. 대부분의 데이터베이스를 사용 하는 코드를 작성 하는 경우 중요 하지 않은 최대 성능을 얻도록 및 간소화 된 코딩 및 Entity Framework 시작 하는 테스트 이용할 수 있습니다. 오버 헤드는 EF 성능이 인해 위치가 상황에서 작성 하 고 이상적으로 저장된 프로시저를 호출 하 여 ADO.NET을 사용 하 여 사용자 고유의 쿼리를 실행할 수 있습니다.

"데이터 전송량" 최대한 최소화 하려는 방법을 사용 하 여 데이터베이스에 액세스 합니다. 즉, 더 큰 쿼리 결과 집합이 하나씩 수십 또는 수백 개의 더 작은 대신에 필요한 모든 데이터를 얻을 수 있는, 경우 하는 것이 좋습니다. 예를 들어 목록 학생과 강좌에 등록 해야 할 경우 것이 하나의 조인 쿼리 보다는 학생 들에 게 하나의 쿼리에서 가져오고 각 학생의 코스에 대 한 별도 쿼리 실행에 있는 데이터의 모든 것이 좋습니다.

## <a name="sql-databases-and-the-entity-framework-in-the-fix-it-app"></a>SQL database 및 Fix It 응용 프로그램에서 Entity Framework 사용

Fix It 응용 프로그램에는 `FixItContext` Entity Framework에서 파생 되는 `DbContext` 클래스, 데이터베이스를 식별 하 고 데이터베이스의 테이블을 지정 합니다. 컨텍스트 작업에 대 한 엔터티 집합 (테이블)를 지정 하 고 코드의 컨텍스트에 연결 문자열 이름을 전달 합니다. 해당 이름을 Web.config 파일에 정의 된 연결 문자열을 가리킵니다.

[!code-csharp[Main](data-storage-options/samples/sample1.cs?highlight=4,8)]

연결 문자열을 *Web.config* 파일 (여기서는 로컬 개발 데이터베이스를 가리키는) appdb 라는:

[!code-xml[Main](data-storage-options/samples/sample2.xml?highlight=3)]

Entity Framework 만듭니다는 *FixItTasks* 테이블에 포함 된 속성에 따라는 `FixItTask` 엔터티 클래스입니다. 상속 하지 않습니다 또는 Entity Framework에 종속성이 있는 것을 의미 하는 간단한 POCO (Plain Old CLR Object) 클래스입니다. 하지만 Entity Framework를 기반으로 테이블을 만드는 방법을 알고 및 된 CRUD (만들기-읽기-업데이트-삭제) 작업을 실행 합니다.

[!code-csharp[Main](data-storage-options/samples/sample3.cs)]

![FixItTasks 테이블](data-storage-options/_static/image15.png)

Fix It 응용 프로그램 데이터 저장소로 작업 하는 CRUD 작업에 사용 되는 리포지토리 인터페이스를 포함 합니다.

[!code-csharp[Main](data-storage-options/samples/sample4.cs)]

리포지토리 메서드는 모든 비동기 완전히 비동기 방식으로 데이터에 대 한 모든 액세스를 가능 하도록 확인 합니다.

포함 하 여 데이터를 사용 하려면 저장소 구현 호출 Entity Framework 비동기 메서드 insert의 경우 LINQ 쿼리를 비롯해 업데이트 및 삭제 작업입니다. Fix It 작업을 찾기 위한 코드의 예는 다음과 같습니다.

[!code-csharp[Main](data-storage-options/samples/sample5.cs)]

알 수 없는 다음 일부 타이밍 및 오류 로깅 코드 여기도, 살펴보겠습니다는 나중에 [모니터링 및 원격 분석 장](monitoring-and-telemetry.md)합니다.

<a id="sqliaas"></a>
## <a name="choosing-sql-database-paas-versus-sql-server-in-a-vm-iaas-in-azure"></a>SQL Database (PaaS) 및 Azure에서 VM (IaaS)에서 SQL Server 선택

좋은 점은 SQL Server 및 Azure SQL Database의 핵심 프로그래밍 모델 둘 다 동일한 된다는 점입니다. 두 환경 모두에서 대부분의 동일한 기술 사용할 수 있습니다. 클라우드에서 개발에서 SQL Server 데이터베이스 및 SQL Database 인스턴스를도 사용할 수는, Fix It 응용 프로그램 설정 방법.

대신 실행할 수 있습니다 동일한 SQL Server 클라우드에서 IaaS Vm에 설치 하 여 온-프레미스를 실행 하는. 일부 레거시 응용 프로그램에 대 한 VM에서 SQL Server를 실행 하면 더 나은 솔루션을 수 있습니다. SQL Server 데이터베이스를 전용된 VM에서 실행 되므로 공유 서버에서 실행 되는 SQL database 보다 더 많은 리소스를 사용할 수 있습니다. 즉, SQL Server 데이터베이스를 더 큰 수 있고 아직 잘 수행 합니다. 일반적으로 작을수록 데이터베이스 크기 및 테이블 크기를 잘 사용 사례에 적합 SQL Database (PaaS) 합니다.

두 가지 모델 중에서 선택 하는 방법에 몇 가지 지침은 다음과 같습니다.

| Azure SQL Database (PaaS) | 가상 컴퓨터 (IaaS)에서 SQL Server |
| --- | --- |
| **전문가** -만들기 또는 Vm을 관리, 업데이트 또는 운영 체제 또는 SQL; 패치 필요가 없습니다 Azure는이 있습니다. -기본 제공 고가용성, 데이터베이스 수준 SLA 사용 하 여 합니다. -(라이선스 필요) 사용에 대해서만 요금을 지급 하므로 총 소유 비용 (TCO) 부족 합니다. -많은 수의 작은 데이터베이스를 처리 하기 위한 적절 한 (&lt;각각 크기가 500gb =) 합니다. -동적으로 쉽게 만들 수 있도록 새 데이터베이스 규모가 확장 됩니다. | ***전문가*** -온-프레미스 SQL Server와 호환 되는 기능입니다. -SQL Server 구현 수 [AlwaysOn 통해 고가용성](https://www.microsoft.com/sqlserver/solutions-technologies/mission-critical-operations/high-availability.aspx) VM 수준 SLA 사용 하 여 2 + Vm에서. -SQL 관리 되는 방식을 완전히 제어를 해야 합니다. -이미 소유한 또는 한 시간 단위로 요금을 지불 하는 SQL 라이선스를 다시 사용할 수 있습니다. -적은 처리에 대 한 적절 한 클 (1 TB +) 데이터베이스입니다. |
| **단점** -온-프레미스 SQL Server에 비해 간격 일부 기능 (부족 [CLR 통합](https://technet.microsoft.com/library/ms131102.aspx)를 [TDE](https://technet.microsoft.com/library/bb934049.aspx)를 [압축 지원](https://technet.microsoft.com/library/cc280449.aspx), [SQL Server Reporting Services](https://technet.microsoft.com/library/ms159106.aspx)등)-500GB의 데이터베이스 크기 제한 합니다. | ***단점*** -업데이트/패치 (OS 및 SQL)은 사용자의 책임-만들기 및 관리 db은 사용자의 책임-디스크 IOPS (초당 입/출력 작업) (16 개 데이터 드라이브)를 통해 8000에 대 한 제한입니다. |

VM에서 SQL Server를 사용 하려는 경우 사용자 고유의 SQL Server 라이선스를 사용할 수 있습니다 또는 한 시간 단위로 요금을 지불할 수 있습니다. 예를 들어, 포털 또는 REST API를 통해 SQL Server 이미지를 사용 하 여 새 VM을 만들 수 있습니다.

![SQL Server를 사용 하 여 VM 만들기](data-storage-options/_static/image16.png)

![SQL Server VM 이미지 목록](data-storage-options/_static/image17.png)

때 VM을 만들 일할 SQL Server 이미지를 사용 하 여 SQL Server 라이선스 비용의 VM 사용량에 따라 시간 단위로 합니다. 몇 달에 대 한 실행 뿐 이라고 하는 프로젝트에 있는 경우 시간 단위로 요금을 지불 하는 저렴 한 것입니다. 프로젝트가 오랫동안 지속 될 것이 있다면 일반적으로 수행 하는 방법은 라이선스를 구입 하는 저렴 한 것입니다.

## <a name="summary"></a>요약

클라우드 컴퓨팅을 혼합할 수 있게 하 고 가장 잘 일치 데이터 저장소 접근 방식에는 응용 프로그램의 요구 사항을 충족 합니다. 새 응용 프로그램을 빌드하는 경우 계속 응용 프로그램 증가 하는 경우에 잘 작동 하는 방법을 선택 하기 위해 여기에 나열 된 질문에 대 한 신중 하 게 생각 합니다. 합니다 [다음 장에서](data-partitioning-strategies.md) 에서는 다양 한 데이터 저장소 접근 방식이 결합 하는 데 사용할 수 있는 몇 가지 분할 전략에 설명 합니다.

## <a name="resources"></a>자료

자세한 내용은 다음 리소스를 참조하세요.

데이터베이스 플랫폼을 선택 합니다.

- [확장성이 뛰어난 솔루션에 대 한 데이터 액세스: SQL, NoSQL 및 Polyglot 지 속성을 사용 하 여](http://aka.ms/dag-doc)입니다. 전자책 Microsoft Patterns and Practices에서 깊이에서 여러 종류의 데이터를 이동 하는 클라우드 응용 프로그램에 사용할 수 있는 저장 합니다.
- [Microsoft Patterns and Practices-Azure 지침](https://msdn.microsoft.com/library/ff898430.aspx)합니다. 데이터 일관성 입문서, 데이터 복제 및 동기화 지침, 인덱스 테이블 패턴, 구체화 된 뷰 패턴을 참조 하세요.
- [기본: Acid 대신](http://queue.acm.org/detail.cfm?id=1394128)합니다. 데이터 일관성 및 확장성에 대 한 절충에 대 한 문서.
- [7 7 주 데이터베이스: 최신 데이터베이스 및 NoSQL 이동 가이드](https://www.amazon.com/Seven-Databases-Weeks-Modern-Movement/dp/1934356921)합니다. 책인 Eric 레드먼드와 R. Jim Wilson입니다. 현재 사용할 수 있는 데이터 저장소 플랫폼의 범위에 직접 도입 하는 데 적극 권장 합니다.

SQL Server 및 SQL Database 중에서 선택 합니다.

- [SQL Database 지침 용 premium 프리뷰](https://msdn.microsoft.com/library/windowsazure/dn369873.aspx)합니다. SQL Database Premium SQL Database Web 및 Business edition을 통해 선택 하는 경우에 대 한 지침을 소개 합니다.
- [지침 및 제한 사항 (Azure SQL Database)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)합니다. SQL Database의 제한 사항에 대 한 설명서 링크는 포털 페이지에서 SQL Database는 SQL Server 기능을 집중 하는 포함 하 여 지원 하지 않습니다.
- [Azure Virtual Machines의 SQL Server](https://msdn.microsoft.com/library/windowsazure/jj823132.aspx)합니다. Azure에서 SQL Server를 실행 하는 방법에 대 한 설명서를 연결 하는 포털 페이지입니다.
- [Scott Guthrie의 Azure SQL Database에 설명](https://azure.microsoft.com/documentation/videos/sql-in-azure-scottgu/)합니다. Scott Guthrie 하 여 SQL Database 6 분짜리 비디오 소개 합니다.
- [응용 프로그램 패턴 및 Azure Virtual Machines의 SQL Server에 대 한 개발 전략](https://msdn.microsoft.com/library/windowsazure/dn574746.aspx)합니다.

Entity Framework 및 SQL Database를 사용 하 여 ASP.NET 웹 앱에서

- [MVC 5를 사용 하 여 EF 6 시작](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다. 9 부 자습서 시리즈는 EF를 사용 하 여 Azure 및 SQL Database에 데이터베이스를 배포 하는 MVC 앱을 빌드하는 것을 안내 합니다.
- [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../../../../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)합니다. 12 부 자습서 시리즈 EF Code First를 사용 하 여 데이터베이스를 배포 하는 방법에 대 한 더 심층적으로 이동 하는 합니다.
- [Azure 웹 사이트에 멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET MVC 5 앱 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)합니다. 단계별 자습서는 웹 앱 만들기를 안내 하는 인증을 사용 하 여, 응용 프로그램 테이블 멤버 자격 데이터베이스에 저장, 데이터베이스 스키마를 수정 및 Azure에 앱을 배포 합니다.
- [ASP.NET 데이터 액세스 콘텐츠 맵](https://go.microsoft.com/fwlink/p/?LinkId=282414)합니다. EF 및 SQL Database를 사용 하 여 작업에 대 한 리소스에 연결 합니다.

Azure에서 MongoDB를 사용합니다.

- [MongoLab-Azure에서 MongoDB](http://msopentech.com/opentech-projects/mongolab-mongodb-on-windows-azure/)합니다. Azure에서 MongoDB를 실행 하는 방법에 대 한 설명서에 대 한 포털 페이지입니다.
- [Azure의 가상 머신에서 실행 되는 MongoDB에 연결 하는 Azure 웹 사이트 만들기](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-store-data-mongodb-vm/)합니다. ASP.NET 웹 응용 프로그램에서 MongoDB 데이터베이스를 사용 하는 방법을 보여 주는 단계별 자습서입니다.

HDInsight (Azure의 Hadoop):

- [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/)합니다. 포털에서 HDInsight 설명서의 [Azure](https://azure.microsoft.com/) 웹 사이트입니다.
- [Hadoop 및 HDInsight: Azure에서 빅 데이터](https://msdn.microsoft.com/magazine/dn385705.aspx)입니다. MSDN Magazine 기사 Bruno Terkaly 및 Ricardo Villalobos, Azure에서 Hadoop을 소개 합니다.
- [Microsoft Patterns and Practices-Azure 지침](https://msdn.microsoft.com/library/dn568099.aspx)합니다. MapReduce 패턴을 참조 하십시오.

> [!div class="step-by-step"]
> [이전](single-sign-on.md)
> [다음](data-partitioning-strategies.md)
