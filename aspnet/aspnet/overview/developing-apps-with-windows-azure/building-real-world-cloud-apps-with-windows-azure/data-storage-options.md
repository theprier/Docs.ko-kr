---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options
title: "데이터 저장소 옵션 (Azure로 응용 프로그램 빌딩 실제 클라우드) | Microsoft Docs"
author: MikeWasson
description: "실제 세계 클라우드로 응용 프로그램 빌딩 Azure 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴 및 그을 수 있는 방법에 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/12/2014
ms.topic: article
ms.assetid: e51fcecb-cb33-4f9e-8428-6d2b3d0fe1bf
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options
msc.type: authoredcontent
ms.openlocfilehash: 88f57244bfbfdf33df3bb265d8aa2c93689b2f24
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="data-storage-options-building-real-world-cloud-apps-with-azure"></a>데이터 저장소 옵션 (Azure로 응용 프로그램 빌딩 실제 클라우드)
====================
여 [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **실제 세계 클라우드로 응용 프로그램 빌딩 Azure** 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴에 설명 하 고 사례 수 있는 클라우드에 대 한 웹 앱을 개발 성공적으로 수행 되어야 합니다. 전자책에 대 한 정보를 참조 하십시오. [첫 번째 장](introduction.md)합니다.


클라우드 앱을 디자인 하 고 될 때 다른 데이터 저장소 옵션을 간과 경향이 및 대부분의 사람들이 관계형 데이터베이스에 사용 됩니다. 표시 될 수 있습니다 만족 스 럽 지 성능, 높은 비용 또는 나타낼지, 때문에 [NoSQL](http://en.wikipedia.org/wiki/NoSQL) (비관계형) 데이터베이스는 몇 가지 작업을 관계형 데이터베이스 보다 더 효율적으로 처리할 수 있습니다. 고객에 대 한 중요 한 데이터 저장소 문제를 해결 하는 도움말 문의 경우에 종종 관계형 데이터베이스를 설정 하는 위치 중 NoSQL 옵션은 동작 더 잘이 했기 때문에 있습니다. 이러한 상황에서는 고객 것 유용한 NoSQL 솔루션 프로덕션 환경에 앱을 배포 하기 전에 구현한 것입니다.

반면에 NoSQL 데이터베이스 할 수 있는 모든 내용을 잘 또는 적절 하 게 생각 하는 것에 잘못 된 것입니다. 단일 최상의 데이터 관리에 대 한 모든 데이터 저장소 작업; 다른 데이터 관리 솔루션은 다양 한 작업에 최적화 됩니다. 대부분의 실제 클라우드 앱 다양 한 데이터 저장소 요구 사항 및 여러 데이터 저장소 솔루션의 조합으로 가장 자주 제공 됩니다.

이 장의 목적은 클라우드 앱 시나리오에 맞는 선택 하는 방법에 대 한 몇 가지 기본 지침을 사용할 수 있는 데이터 저장소 옵션 보다 광범위 한 의미를 부여 하는 것입니다. 검토가 필요 장단점에 대 한 응용 프로그램을 개발 하 고 사용할 수 있는 옵션에 주의 해야 하는 것이 좋습니다. 프로덕션 응용 프로그램에서 데이터 저장소 옵션을 변경 하는 평면 처리 중인 동안 jet 엔진을 변경 하지와 같은 매우 어려울 수 있습니다.

## <a name="data-storage-options-on-azure"></a>Azure에서 데이터 저장소 옵션

클라우드를 사용 하면 비교적 쉽게 다양 한 관계형 및 NoSQL 데이터 저장소를 사용할 수 있습니다. 다음은 Azure에서 사용할 수 있는 데이터 저장소 플랫폼의 일부입니다.

![](data-storage-options/_static/image1.png)

다음 표에서 네 가지 유형의 NoSQL 데이터베이스를 보여줍니다.

- [키/값 데이터베이스](https://msdn.microsoft.com/library/dn313285.aspx#sec7) 각 키 값에 대 한 단일 직렬화 된 개체를 저장 합니다. 대용량의 위치 지정된 된 키 값에 대 한 하나의 항목을 가져올 없는 데이터를 저장 하기 위한 값비싼 기반 항목의 다른 속성으로 쿼리 합니다.

    [Azure Blob 저장소](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/) 파일 저장소 폴더와 파일 이름에 해당 하는 키 값을 가진 클라우드에서 처럼 작동 하는 키/값 데이터베이스입니다. 해당 폴더와 파일 이름에 의해 값 파일 내용에 대 한 검색 파일을 검색 합니다.

    [Azure 테이블 저장소](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/) 키/값 데이터베이스 이기도 합니다. 각 값에 호출 되는 *엔터티* (파티션 키와 행 키로 식별 되는 행과 유사) 여러 개 포함 된 및 *속성* (열과 비슷하지만 되지만 테이블의 모든 엔터티가 동일한 공유 해야 하는 경우 열)입니다. 이 아닌 키 열에서 쿼리는 비효율적 있으며 피해 야 합니다. 예를 들어 단일 사용자에 대 한 정보를 저장 하는 하나의 파티션 사용자 프로필 데이터를 저장할 수 있습니다. 동일한 파티션에 별도 엔터티 또는 별도 한 엔터티의 속성을에 사용자 이름과 암호 해시, 생년월일, 등의 데이터를 저장할 수 있습니다. 하지만 생년월일의 지정된 된 범위에 있는 모든 사용자에 대 한 쿼리 하려는 없게 하 고 사용자 프로필 테이블과 다른 테이블 간의 조인 쿼리를 실행할 수 없습니다. 테이블 저장소 확장성이 뛰어난 하 고 관계형 데이터베이스에 비해 저렴 하지만 복잡 한 쿼리 또는 조인을 사용 하지 않습니다.
- [Documentdatabases](https://msdn.microsoft.com/library/dn313285.aspx#sec8) 값이 있는 키/값 데이터베이스가 *문서*합니다. "문서" 여기 Word 또는 Excel 문서 의미에서 사용 되지 않습니다 되지만 명명 된 필드와 하위 문서 될 수 있는 값의 컬렉션을 의미 합니다. 예를 들어 주문 기록 테이블에 주문 문서 해야할 주문 번호, 주문 날짜 및 고객 필드입니다. 및 고객 필드 이름 및 주소 필드가 있을 수 있습니다. 데이터베이스 필드 형식으로 데이터를를 XML, YAML, JSON, 또는 BSON; 같은 인코딩합니다. 또는 일반 텍스트를 사용할 수 있습니다. 키/값 데이터베이스와는 별도로 문서 데이터베이스를 설정 하는 기능 중 하나는 키가 아닌 필드에서 쿼리를 쿼리할 수 있도록 보다 효율적인 보조 인덱스를 정의 하는 기능이 있습니다. 이 기능은 문서 키의 값 보다 더 복잡 한 조건에 따라 데이터를 검색 해야 하는 응용 프로그램에 보다 적합 한 문서 데이터베이스를 만듭니다. 예를 들어 판매 주문 기록 문서 데이터베이스에서 제품 ID, 고객 ID, 고객 이름, 등과 같은 다양 한 필드에 쿼리하여 수 있습니다. [MongoDB](http://www.mongodb.org/) 인기 있는 문서 데이터베이스입니다.
- [열-제품군 데이터베이스](https://msdn.microsoft.com/library/dn313285.aspx#sec9) 키/값 데이터 저장소를 열 패밀리를 호출 하는 관련 열의 컬렉션으로 구조를 데이터 저장소에 사용 하면 됩니다. 예를 들어 인구 조사 데이터베이스 하나의 개인의 이름에 대 한 열 그룹을 해야할 (첫째, 중간 이름, 성)을 사용자의 주소에 대 한 그룹 및 사용자의 프로필 정보 (DOB, 성별, 등)에 대 한 한 개의 그룹입니다. 데이터베이스를 별도 파티션으로 열 패밀리마다 동일한 키와 관련 한 사용자의 데이터를 모두 유지 하면서 저장한 다음 수 있습니다. 그런 다음 모든 이름 및 주소 정보를 읽지 않고 모든 프로필 정보를 읽을 수 있습니다. [Cassandra](http://cassandra.apache.org/) 인기 열 제품군 데이터베이스입니다.
- [데이터베이스를 그래프로](https://msdn.microsoft.com/library/dn313285.aspx#sec10) 개체 및 관계의 컬렉션으로 정보를 저장 합니다. 그래프 데이터베이스의 목적은 응용 프로그램을 서로 개체와는 관계의 네트워크를 트래버스해야 하는 쿼리를 효율적으로 수행할 수 있도록 합니다. 예를 들어 인사 데이터베이스의 직원의 개체 수 했는데 할 수 있습니다 용이 하 게 하려면 쿼리와 같은 "직접 또는 간접적으로 작업 하는 모든 직원 scott." [Neo4j](http://www.neo4j.org/) 인기 있는 그래프 데이터베이스입니다.

관계형 데이터베이스에 비해, NoSQL 옵션 훨씬 큰 확장성과 저장 및 구조화 되지 않은 데이터 분석에 대 한 비용 효율성을 제공 합니다. 이 경우 단점이 풍부한 queryability 및 관계형 데이터베이스의 강력한 데이터 무결성 기능을 제공 하지 마세요. NoSQL 조인 쿼리 필요 없이 많은 볼륨을 포함 하는 IIS 로그 데이터에 대 한 잘 작동 합니다. NoSQL가 작동 하지 않는 에서도 완벽 하 게 뱅킹 트랜잭션과, 절대 데이터 무결성 필요 하 고 다른 계정 관련 데이터에 여러 관계가 포함 됩니다.

또한 호출 하는 데이터베이스 플랫폼의 최신 범주 [NewSQL](http://en.wikipedia.org/wiki/NewSQL) queryability 및 관계형 데이터베이스의 트랜잭션 무결성 NoSQL 데이터베이스의 확장성을 결합 하는 합니다. NewSQL 데이터베이스는 분산된 된 저장소 및 쿼리 처리 하는 경우가 많습니다 "OldSQL" 데이터베이스에 구현 하기 위한 것입니다. [NuoDB](http://www.nuodb.com/) 은 Azure에서 사용할 수 있는 NewSQL 데이터베이스의 예입니다.

<a id="hadoop"></a>
## <a name="hadoop-and-mapreduce"></a>Hadoop 및 MapReduce

대용량 NoSQL 데이터베이스에 저장할 수 있는 데이터의 제때에 효과적으로 이해 하기 어려울 수 있습니다. 와 같은 프레임 워크를 사용할 수 있는 작업을 수행 하 [Hadoop](http://hadoop.apache.org/) 구현 하는 [MapReduce](http://en.wikipedia.org/wiki/MapReduce) 기능입니다. 기본적으로 MapReduce 프로세스는 다음과 같습니다.

- 만 분석 해야 하는 실제로 데이터를 저장 하는 한 데이터를 선택 하 여 처리 하는 데이터의 크기를 제한 합니다. 예를 들어, 사용자 프로필 데이터 저장소에서 출생 연도 선택 하므로 출생 연도 여 사용자층의 구성을 확인 하려면.
- 부분으로 데이터를 구분 하 고 처리를 위해 다른 컴퓨터로 보내야 합니다. 1950 1959 날짜 있는 사용자의 수를 계산 하는 컴퓨터 A, b가 1960 1969, 등입니다. 이 컴퓨터 그룹 라고는 *Hadoop 클러스터*합니다.
- 부분에 처리를 완료 한 후 각 부분의 결과 다시 함께 포함 합니다. 비교적 짧은 목록이 각 출생 연도 대 한 개수 사람 있으며이 전체 목록에는 백분율 계산 하는 작업은 관리할 수 있습니다.

Azure에서 [HDInsight](https://azure.microsoft.com/services/hdinsight/) 처리, 분석 및 Hadoop의 기능을 사용 하 여 빅 데이터에서 새로운 통찰력을 얻을 수 있습니다. 예를 들어 웹 서버 로그 분석에 사용할 수 있습니다.

- 저장소 계정에 웹 서버 로깅을 사용 하도록 설정 합니다. 이 응용 프로그램에 모든 HTTP 요청에 대해 Blob 서비스에 로그가 기록 Azure를 설정 합니다. Blob 서비스는 기본적으로 클라우드 파일 저장소 및 HDInsight와 원활 하 게 통합 합니다. 

    ![Blob 저장소에 로그](data-storage-options/_static/image2.png)
- 앱 트래픽 가져옵니다, 웹 서버 IIS 로그 Blob 저장소에 작성 됩니다. 

    ![웹 서버 로그](data-storage-options/_static/image3.png)
- 포털에서 클릭 **새로** - **데이터 서비스** - **HDInsight** - **빠른 생성**, 고 HDInsight 클러스터 이름, 클러스터 크기 (HDInsight 클러스터 데이터 노드 수) 및 사용자 이름 및 HDInsight 클러스터에 대 한 암호를 지정 합니다. 

    ![HDInsight](data-storage-options/_static/image4.png)

이제 MapReduce 작업을 로그 분석 하 고와 같은 질문에 대 한 답을 얻을를 설정할 수 있습니다.

- 하루 중 어떤 시간이이 응용 프로그램 가져오기 최대 또는 최소 트래픽
- 어떤 국가에서 오는 내 트래픽 인가요?
- 내 트래픽에서 가져온 영역의 평균 환경 수입 이란 합니다. (IP 주소를 통해 환경 수입을 제공 하는 공용 데이터 집합은 및 웹 서버 로그에서 IP 주소에 대해를 찾아 볼 수 있습니다.)
- 특정 페이지 또는 사이트에서 제품을 환경 소득 파악 하는 방법

그런 다음 고객에 관심이 있을 수 가능성에 따라 또는 특정 제품을 구입할 가능성이 높은 대상 광고에 이와 같은 질문에 대 한 답변을 사용할 수 있습니다.

에 설명 된 대로 [장 모든 자동화](automate-everything.md), 포털에서 수행할 수 있는 대부분의 함수를 자동화할 수 있습니다 및을 설정 하 고 실행 중인 작업을 분석 하는 HDInsight 포함 합니다. 일반적인 HDInsight 스크립트는 다음 단계를 포함할 수 있습니다.

- HDInsight 클러스터를 프로 비전 하 고 Blob 저장소 입력에 대 한 저장소 계정에 연결 합니다.
- HDInsight 클러스터를 MapReduce 작업 실행 파일 (.jar 또는.exe 파일)를 업로드 합니다.
- Blob 저장소에 출력 데이터를 저장 하는 MapReduce 제출 합니다.
- 작업이 완료 될 때까지 기다립니다.
- HDInsight 클러스터를 삭제 합니다.
- Blob 저장소에서 출력에 액세스 합니다.

이 모든 작업을 수행 하는 스크립트를 실행 하 여 비용을 최소화 하는 HDInsight 클러스터를 프로 비전 하는 시간의 양을 최소화 합니다.

<a id="paasiaas"></a>
## <a name="platform-as-a-service-paas-versus-infrastructure-as-a-service-iaas"></a>서비스 (IaaS) 인프라와 서비스 (PaaS) 플랫폼

데이터 저장소 옵션 앞에 나열 된 플랫폼으로-서비스 (PaaS) 및 인프라-as a Service (IaaS) 솔루션을 모두 포함 됩니다. PaaS는 하드웨어 및 소프트웨어 인프라를 관리 합니까 서비스 사용을 의미 합니다. SQL 데이터베이스에는 azure PaaS 기능입니다. 데이터베이스에 대 한 요청 및 원리를 자세히 파악할수록 Azure를 설정 하 고 Vm을 구성 하 고에 데이터베이스를 설정 합니다. Vm에 직접 액세스할 수 없는 하 고 관리할 필요가 없습니다. 에 원하는 작업이 무엇이 든 배치를 설정, 구성 및 데이터 센터 인프라를를 실행 하는 Vm 관리 IaaS 의미 합니다. 일반적인 VM 구성에 대해 미리 구성 된 VM 이미지의 갤러리를 제공합니다. 예를 들어 Windows Server 2008, Windows Server 2012, BizTalk Server, Oracle WebLogic Server, Oracle 데이터베이스 등 미리 구성 된 VM 이미지를 설치할 수 있습니다.

Azure에서 제공 하는 PaaS 데이터 솔루션은 다음과 같습니다.

- Azure SQL 데이터베이스 (이전의 SQL Azure)입니다. SQL Server에 기반 하는 클라우드 관계형 데이터베이스입니다.
- Azure 테이블 저장소입니다. 키/값 NoSQL 데이터베이스입니다.
- Azure Blob storage. 클라우드 저장소를 파일입니다.

IaaS에 대 한 예는 VM에 로드할 수 아무 것도 실행할 수 있습니다.

- SQL Server, Oracle, MySQL, SQL Compact, SQLite 또는 Postgres와 같은 관계형 데이터베이스입니다.
- Memcached, Redis, Cassandra, 및 Riak 같은 데이터 저장소에 키/값입니다.
- HBase 같은 열 데이터를 저장합니다.
- MongoDB, RavenDB, 및 CouchDB 같은 데이터베이스를 문서화 합니다.
- Neo4j 같은 데이터베이스를 그래프로 표시 합니다.

![Azure에서 데이터 저장소 옵션](data-storage-options/_static/image5.png)

IaaS 옵션 거의 무제한 데이터 요금 저장소 옵션을 제공 및 미리 구성 된 이미지를 사용 하 여 Vm을 만들 수 있기 때문에 그 중 대부분은 특히 사용 하기 쉽습니다. 예를 들어 관리 포털에서로 이동 **가상 컴퓨터**, 클릭는 **이미지** 탭을 클릭 **VM Depot 찾아보기를**합니다.

![VM Depot 찾아보기](data-storage-options/_static/image6.png)

목록을 표시 [미리 구성 된 VM 이미지에서 수백](http://www.hanselman.com/blog/Over400VirtualMachineImagesOfOpenSourceSoftwareStacksInTheVMDepotAzureGallery.aspx), MongoDB, Neo4J, Redis, Cassandra, 또는 CouchDB 등 데이터베이스 관리 시스템 미리 설치 된 이미지에서 VM을 만들 수 있습니다.

![VM Depot에서 MongoDB](data-storage-options/_static/image7.png)

Azure IaaS 데이터 저장소 옵션 최대한 사용 하기 쉬운 하지만 PaaS 제품 몇 가지 더 비용 효율적이 고 다양 한 시나리오에 대 한 실용적인 하는 많은 이점이 있습니다.

- Vm을 만들 필요가 없습니다 방금 데이터 저장소를 설정 하는 포털 또는 스크립트를 사용 합니다. 200 테라바이트 데이터 저장소를 사용 하도록 하려는 경우 수만 단추를 클릭 하거나, 명령을 실행 하 고 시간 (초)에는 사용할 수 있습니다.
- 관리 또는 서비스에서 사용 하는 Vm 패치 필요가 없습니다. Microsoft에서 사용자에 대 한 자동으로.-크기 조정 또는 높은 가용성;에 대 한 인프라를 설정 하는 방법에 대 한 중요 하지 않은 Microsoft는 사용자에 대 한 모든 작업을 처리합니다.
- 라이선스를 구입할 필요가 없습니다. 사용료는 서비스 비용에 포함 됩니다.
- 만 사용 하는 것에 대 한 지불 합니다.

Azure에서 PaaS 데이터 저장소 옵션에서 타사 공급자가 제공은 포함 합니다. 예를 들어 선택할 수 있습니다는 [MongoLab 추가 기능](https://azure.microsoft.com/documentation/articles/store-mongolab-web-sites-dotnet-store-data-mongodb/) 서비스로 MongoDB 데이터베이스 프로 비전 하 고 Azure Store에서 합니다.

## <a name="choosing-a-data-storage-option"></a>데이터 저장소 옵션을 선택합니다.

모든 시나리오에 적합 한 한 가지 방법은 없습니다. 누구나 라는 경우이 기술을 대답 먼저에 게 문의 하십시오 점은 "란 질문?", 다양 한 솔루션은 다른 작업에 최적화 되어 있습니다. 즉, 관계형 모델에 한 정적 이점이 있습니다. 바로 이러한 이유로 오랫동안 동안 주위 되었습니다. 하지만 NoSQL 솔루션으로 해결할 수 있는 sql 다운 양쪽도 있습니다.

종종 보이는 가장은 단일 솔루션에서 SQL 및 NoSQL 사용 되는 위치를 compositional 접근 방법입니다. 도 때 사람들 말은 수용 하 NoSQL, 기능 작동 상태 있습니다 종종 드릴 하는 경우 여러 다른 NoSQL 프레임 워크를 사용 하는 찾기: 사용 중인 [CouchDB](http://wiki.apache.org/couchdb/Introduction), 및 [Redis](http://redis.io/), 및 [ Riak](http://basho.com/riak/) 서로 다른 작업에 대 한 합니다. 짝수 Facebook NoSQL를 광범위 하 게 사용 하는 서비스의 다른 부분에 대 한 다양 한 NoSQL 프레임 워크를 사용 합니다. 데이터 저장소 접근 방식으로 섞어서 유연성의 클라우드에 대 한 여러 데이터 솔루션을 사용 하는 단일 앱에 통합 하는 것이 쉽습니다 하는 것 중 하나입니다.

다음은 한 방법을 선택할 때 고려할 몇 가지 질문입니다.

| 의미 체계 데이터 | -이란 의미 체계 핵심 데이터 저장소 및 데이터 액세스 (사용자 데이터를 저장할 관계형 또는 구조화 되지 않은)? Blob 저장소;에 가장 적합 한 미디어 파일과 같은 구조화 되지 않은 데이터 제품, 인벤토리, 공급자, 고객 주문 등과 같은 관련된 데이터의 컬렉션에는 관계형 데이터베이스에 가장 적합 합니다. |
| --- | --- |
| 쿼리 지원 | -얼마나 쉬운지는 데이터를 쿼리하려면 없나요? -질문 수 있는 유형을 효율적으로 요청? 키/값 데이터 저장소는 키 값을 지정 된 단일 행을 가져오는에 적합 하지만 복잡 한 쿼리에서 유용 하지 않습니다. 사용자 프로필 데이터 저장소를 항상 가져오는지 하나의 특정 사용자에 대 한 데이터에 대 한 키/값 데이터 저장소 수 제대로 작동 합니다. 다양 한 제품 특성을 기반으로 하는 다른 그룹 가져오려는 제품 카탈로그에 대 한 관계형 데이터베이스는 더 적합할 수 있습니다. NoSQL 데이터베이스 많은 양의 데이터를 효율적으로 저장할 수 있지만 응용 프로그램에서 데이터를 쿼리 하는 방법을 주위 데이터베이스를 구성 하 있고이 하면 임시 쿼리 작업을 수행 하는 어렵습니다. 관계형 데이터베이스와 함께 거의 모든 종류의 쿼리를 작성할 수 있습니다. |
| 기능 프로젝션 | -질문 수, 집계 등, 여야 실행 된 서버 쪽? SELECT COUNT를 실행 하는 경우 (\*) SQL에서 테이블을 매우 효율적으로 서버에서 모든 작업을 수행 하 고 숫자을 찾고 반환 합니다. 집계를 지원 하지 않는 NoSQL 데이터 저장소에서 동일한 계산을 원하는 경우이 비효율적인 "unbounded 쿼리" 이며 아마도 시간이 초과 됩니다. 쿼리가 성공 하면 경우에를 클라이언트에 서버에서 데이터를 모두 검색 하 고 클라이언트에 행을 계산 해야 합니다. -어떤 언어 또는 유형의 식 사용할 수 있습니다. SQL 관계형 데이터베이스와 함께 사용할 수 있습니다. Azure 테이블 저장소와 같은 일부 NoSQL 데이터베이스와 함께 사용 [OData](http://www.odata.org/), 제가 할 수 있는 모든는 기본 키에서 필터링으로 프로젝션 (사용 가능한 필드의 하위 집합을 선택 합니다.)를 가져옵니다. |
| 확장의 용이성 | -간격과 비용 데이터 해야 하나요? 확장은 플랫폼에서 고유 하 게 구현? -하기가 쉽습니까 (크기 및 처리량) 용량 추가/제거? 관계형 데이터베이스 및 테이블 되지 특정 제한 이상으로 늘리려면 어려운 되기 때문 확장 가능 하면 자동으로 분할 합니다. Azure 테이블 저장소와 같은 NoSQL 데이터 저장소를 기본적으로 모든 항목 분할 되며 파티션을 추가에 제한이 거의 없습니다. 200 테라바이트 테이블 저장소를 쉽게 확장할 수 있지만 Azure SQL 데이터베이스에 대 한 최대 데이터베이스 크기는 500 (기가바이트). 여러 데이터베이스로 분할 하 여 관계형 데이터를 확장할 수 있지만 많은 프로그래밍 작업을 수행 해야 해당 모델을 지원 하도록 응용 프로그램을 설정 합니다. |
| 계측 및 관리 효율성 | -계측, 모니터링 및 관리 하는 플랫폼 얼마나 쉬운지 인가요? 플랫폼을 무료로 제공 대상 메트릭 들겠지만 알아야 할 하므로 상태 및 데이터 저장소의 성능에 대 한 정보를 유지 해야 하며, 사용자가 직접 개발 하 해야 합니다. |
| 작업 | -얼마나 쉽게 배포 하 고 Azure에서 실행 플랫폼 이란 인가요? PaaS? IaaS? Linux? 테이블 저장소 및 SQL 데이터베이스는 Azure에서 설정할 수 있습니다. 기본 제공 Azure PaaS 솔루션 되지 않는 플랫폼에 더 많은 노력이 필요 합니다. |
| API 지원 | -쉽게 플랫폼을 사용 하는 API 사용할 수 있는? Azure 테이블 서비스에 대 한.NET 4.5 비동기 프로그래밍 모델을 지 원하는.NET API와 SDK 있습니다. .NET 응용 프로그램을 작성 하는 경우 훨씬 쉽게 작성 하 고 API가 없습니다. 또는 소규모 하나 있는 다른 키/값 열 데이터 저장소 플랫폼에 비해 Azure 테이블 서비스에 대 한 코드를 테스트할 수 있습니다. |
| 트랜잭션 무결성 및 데이터 일관성 | -는 중요 한 데이터 일관성을 유지 하려면 플랫폼에서 트랜잭션을 지원는 무엇입니까? 대량 전자 메일이 전송 된 성능 및 낮은 데이터 저장소 비용 트랜잭션이나 데이터 플랫폼의 참조 무결성에 대 한 자동 지원 보다 더 중요할 수 있습니다는 추적에 대 한 Azure 테이블 서비스에 적합 한 선택이 있도록 합니다. 은행 계좌 추적에 대 한 균형을 조정 하거나 구매 주문서 트랜잭션 되도록 보장에 더 적합할 수는 제공 하는 관계형 데이터베이스 플랫폼입니다. |
| 비즈니스 연속성 | -얼마나 쉬운지? 백업, 복원 및 재해 복구 프로덕션 데이터는 손상 조만간 및 실행 취소 함수는 필요 합니다. 관계형 데이터베이스를 지정 시간으로 복원 하는 등의 많은 세분화 된 복원을 기능 있는 경우가 많습니다. 고려해 야 할 중요 한 요소는 고려 하는 각 플랫폼에서 사용할 수 있는 복원 기능을 이해 합니다. |
| 비용 | -둘 이상의 플랫폼 데이터 작업에서 지원할 수 있는 경우 이러한 비교 하면 어떻게 비용? 예를 들어 ASP.NET Identity를 사용 하는 경우 Azure 테이블 서비스 또는 Azure SQL 데이터베이스에서 사용자 프로필 데이터를 저장할 수 있습니다. SQL 데이터베이스의 기능을 쿼리 하는 풍부한 필요 하지 않으면를 선택할 수 있습니다 Azure 테이블을 부분적으로 많은 비용이 소요 하기 때문에 저장소가 주어진된 시간에 대 한 줄어듭니다. |

어떤는 일반적으로 권장은 데이터 저장소 솔루션을 선택 하기 전에 이러한 각 범주에 있는 질문에 대 한 답변을 알고 있습니다.

또한 작업에는 일부 플랫폼 보다 나은 지원할 수 있는 특정 요구 사항이 있을 수 있습니다. 예:

- 응용 프로그램에 필요한 기능을 감사지 않습니다?
- 데이터 수명 요구 사항은 무엇입니까-자동화 된 보관 또는 제거 기능 필요 하십니까?
- 특수 한 보안 요구 사항이 있습니까? 예를 들어 데이터 PII (개인 식별이 가능한 정보)를 포함 하지만 PII가 쿼리 결과에서 제외 해야 할 수 있어야 합니다.
- 규정 또는 기술적 이유로 클라우드에 저장할 수 없는 일부 데이터가 있는 경우에 온-프레미스 저장소와 통합을 용이 하 게 하는 클라우드 데이터 저장소 플랫폼을 할 수 있습니다.

## <a name="demo--using-sql-database-in-azure"></a>데모 – Azure의 SQL 데이터베이스를 사용 하 여

수정 앱 작업을 저장 하는 관계형 데이터베이스를 사용 합니다. 에 표시 된 환경 만들기 Windows PowerShell 스크립트는 [모든 자동화 장](automate-everything.md) 두 개의 SQL 데이터베이스 인스턴스를 만듭니다. 클릭 하 여 포털에서 볼 수 있습니다는 **SQL 데이터베이스** 탭 합니다.

![포털에서 SQL 데이터베이스](data-storage-options/_static/image8.png)

포털을 사용 하 여 데이터베이스를 만들도 쉽습니다.

클릭 **-새 데이터 서비스** -- **SQL 데이터베이스** -- **빠른 생성**, 데이터베이스 이름, 사용자 계정에 이미 있으면 서버 선택 또는 새 대시보드를 만들고 클릭 **SQL 데이터베이스 만들기**합니다.

![새 SQL Database](data-storage-options/_static/image9.png)

몇 초 동안 기다립니다 있고 데이터베이스에서 Azure를 사용할 수 있습니다.

![만든 새 SQL 데이터베이스](data-storage-options/_static/image10.png)

Azure는 일부에서 초 내에 어떤 걸릴 수 있습니다 있습니다 하루에 있도록 일주일 또는 온-프레미스 환경에서 수행 하는 데 더 많은 합니다. 및 스크립트에서 또는 관리 API를 사용 하 여 자동으로 데이터베이스를 작성할 수 손쉽게를 동적으로 수평 확장할 수 있습니다 < 된 > 데이터베이스에 여러 데이터를 분산 함으로써으로 하는 응용 프로그램 프로그래밍 되었습니다. < /o : p >

이 플랫폼으로-서비스 모델의 예시입니다. 서버를 관리할 필요가 없습니다, 그리고 그렇게 합니다. 백업에 대 한 중요 하지 않은, 그렇게 합니다. 고가용성-에서 실행 되는 데이터베이스의에서 데이터를 자동으로 세 명의 서버에서 복제 됩니다. 소멸 되는 컴퓨터에서는 자동으로 장애 조치 하 고 데이터가 손실 됩니다. 서버는 정기적으로 패치 됩니다, 그리고이 대해 걱정할 필요가 없습니다.

단추를 클릭 하 고 필요 하 고 새 데이터베이스를 사용 하 여 즉시 시작할 수 정확한 연결 문자열을 가져옵니다.

![연결 문자열](data-storage-options/_static/image11.png)

대시보드에 사용 된 저장소의 양과 연결 기록을 보여 줍니다.

![SQL 데이터베이스 대시보드](data-storage-options/_static/image12.png)

SQL Server 도구를 사용 하 여 이미 익숙할 것, SQL Server Management Studio (SSMS) 및 SQL Server 개체 탐색기 (SSOX) 및 서버 탐색기는 Visual Studio 도구를 포함 하 여 또는 포털에서 데이터베이스를 관리할 수 있습니다.

![SSOX](data-storage-options/_static/image13.png)

또 다른 좋은 점은 가격 책정 모델입니다. 20MB 무료 데이터베이스와 함께 개발을 시작할 수 있습니다 및 프로덕션 데이터베이스는 매달 약 $5에서 시작 합니다. 실제로 최대 용량 하지 데이터베이스에 저장 된 데이터에 대해서만 지불 합니다. 라이선스를 구입할 필요가 없습니다.

SQL 데이터베이스는 쉽게 확장 됩니다. 수정 응용 프로그램에 대 한 자동화 스크립트에서 생성 하는 데이터베이스는 1gb 제한 됩니다. 150 기가 최대 크기를 조정 하려는 경우 있습니다 수 방금 포털로 이동 하 고 해당 설정을 변경 또는 REST API 명령을 실행 하며 데이터를 배포할 수 있는 150 기가 데이터베이스 (초)에서 해야 합니다.

![SQL 데이터베이스 버전 및 크기](data-storage-options/_static/image14.png)

신속 하 고 쉽게 인프라를 대기 모드로 전환 하 고 즉시 사용을 시작 하려면 클라우드 기능입니다.

두 SQL 데이터베이스, 멤버 자격 (인증 및 권한 부여) 및 데이터에 대 한 수정 앱을 사용 하 고 프로 비전 하 고 크기를 조정할 때 수행 해야 함. 앞에서 본 포털에서 작업을 수행 하는 것이 얼마나 쉬운지 또한 살펴보았습니다 및 Windows PowerShell 스크립트를 통해 데이터베이스를 프로 비전 하는 방법입니다.

## <a name="entity-framework-versus-direct-database-access-using-adonet"></a>ADO.NET를 사용 하 여 데이터베이스를 직접 액세스와 entity Framework

Entity Framework를 사용 하 여 이러한 데이터베이스를 액세스 하는 수정 응용 프로그램, Microsoft의.NET 응용 프로그램에 ORM (개체 관계형 매퍼)를 권장 합니다. ORM 개발자의 생산성을 용이 하 게 하는 좋은 도구 이지만 일부 시나리오에서 성능이 저하 되 남게 되므로 생산성 합니다. 실제 클라우드 앱에서 EF 또는 ADO.NET를 사용 하 여 직접 사이 선택을 내릴 수 없습니다-둘 다를 사용 합니다. 대부분의 경우 데이터베이스를 사용 하는 코드를 작성 하는 최대 성능을 얻는 중요 하지 않은 및 테스트 등의 간단한 코딩 Entity Framework와 함께 해 서 이용할 수 있습니다. EF 오버 헤드가 성능 인해 위치가 경우에서 작성 및 이상적으로 저장된 프로시저를 호출 하 여 ADO.NET을 사용 하 여 사용자 고유의 쿼리를 실행할 수 있습니다.

"규격화" 가능한 한 최소화 하려는 데이터베이스에 액세스 하려면 사용 하는 방법을 합니다. 즉, 하나의 큰 쿼리 결과 수십 또는 수백 개의 작게 하는 대신 집합에 필요한 모든 데이터를 얻을 수 있는, 경우 되는 것이 좋습니다. 예를 들어 목록 학생과에 등록 하는 과정에 필요한 경우 한 조인 쿼리 보다는 한 쿼리에서 학습자를 가져오는 및 각 학생 과정에 대 한 별도 쿼리 실행에 대 한 데이터를 가져오려는 일반적으로 더 나은 합니다.

## <a name="sql-databases-and-the-entity-framework-in-the-fix-it-app"></a>SQL 데이터베이스 및 수정 응용 프로그램에서 Entity Framework

수정 응용 프로그램에서의 `FixItContext` Entity Framework에서 파생 된 클래스 `DbContext` 클래스, 데이터베이스를 식별 하 고 데이터베이스의 테이블을 지정 합니다. 컨텍스트 작업에 대 한 엔터티 집합 (테이블)을 지정 하 고 코드 전달 컨텍스트에 연결 문자열 이름입니다. 해당 이름은 Web.config 파일에 정의 된 연결 문자열을 가리킵니다.

[!code-csharp[Main](data-storage-options/samples/sample1.cs?highlight=4,8)]

연결 문자열은 *Web.config* 파일 이름이 (로컬 개발 데이터베이스를 가리키는 여기) appdb:

[!code-xml[Main](data-storage-options/samples/sample2.xml?highlight=3)]

Entity Framework 만듭니다는 *FixItTasks* 테이블에 포함 된 속성에 따라는 `FixItTask` 엔터티 클래스입니다. Entity Framework에 대 한 모든 종속성 및에서 상속 하지 않는 것을 의미 하는 간단한 POCO (Plain Old CLR Object) 클래스입니다. 하지만 Entity Framework 기반 테이블을 만드는 방법을 알고와 함께 CRUD (만들기-읽기-업데이트-삭제) 작업을 실행 합니다.

[!code-csharp[Main](data-storage-options/samples/sample3.cs)]

![FixItTasks 테이블](data-storage-options/_static/image15.png)

수정 응용 프로그램 데이터 저장소로 작업 하는 CRUD 작업에 대해 사용 되는 리포지토리 인터페이스를 포함 합니다.

[!code-csharp[Main](data-storage-options/samples/sample4.cs)]

확인할 리포지토리 메서드 모두 비동기 하므로 완전히 비동기 방식으로 데이터에 대 한 모든 액세스를 수행할 수 있습니다.

포함 한 데이터로 작업 하는 저장소 구현 호출 Entity Framework 비동기 메서드 LINQ 쿼리를 비롯해: 삽입, 업데이트 및 삭제 작업. 수정 작업을 찾기 위한 코드의 예를 들면 다음과 같습니다.

[!code-csharp[Main](data-storage-options/samples/sample5.cs)]

일부 타이밍 및 로깅 코드를 여기에 오류가 있어에서 살펴보게는 나중에 알 수는 [모니터링 및 원격 분석 장](monitoring-and-telemetry.md)합니다.

<a id="sqliaas"></a>
## <a name="choosing-sql-database-paas-versus-sql-server-in-a-vm-iaas-in-azure"></a>Azure에서 VM (IaaS)에서 SQL Server와 SQL 데이터베이스 (PaaS)를 선택합니다.

SQL Server 및 Azure SQL 데이터베이스에 대 한 좋을 둘 모두에 대 한 핵심 프로그래밍 모델 동일 된다는 점입니다. 두 환경 모두에서 대부분의 동일한 기술 사용할 수 있습니다. 사용할 수도 있습니다 개발에서 SQL Server 데이터베이스 및 SQL 데이터베이스 인스턴스는 클라우드에서 수정 응용 프로그램 설정 방법 변수인 합니다.

에서 실행할 수 있습니다 동일한 SQL Server 클라우드 IaaS Vm에 설치 하 여 온-프레미스를 실행 합니다. 일부 레거시 응용 프로그램에 대 한 VM에서 SQL Server를 실행 하면 더 나은 수 있습니다. SQL Server 데이터베이스에서는 전용된 VM에서 실행 기 때문에 공유 서버에서 실행 되는 SQL 데이터베이스 데이터베이스 보다 더 많은 리소스를 사용할 수 있습니다. 즉, SQL Server 데이터베이스를 더 큰 수 있으며 여전히 잘 수행 합니다. 일반적으로 값이 작을수록 데이터베이스 크기 및 테이블 크기를 더 사용 사례에서 작동 SQL 데이터베이스 (PaaS) 합니다.

다음은 두 모델 중에서 선택 하는 방법에 몇 가지 지침입니다.

| Azure SQL 데이터베이스 (PaaS) | 가상 컴퓨터 (IaaS)에서 SQL Server |
| --- | --- |
| **전문가** -만들기 또는 Vm 관리, 업데이트 또는 운영 체제 또는 SQL; 패치 필요가 없습니다 Azure 사용자에 대해이 작업이 있습니다. -기본 제공 고가용성을 데이터베이스 수준의 SLA 사용 합니다. -사용 하는 것 (라이선스 필요)에 대해서만 지불 하기 때문에 총 소유 비용 (TCO) 부족 합니다. -좋은 많은 수의 작은 데이터베이스를 처리 하기 위한 (&lt;= 500 GB)입니다. -를 동적으로 쉽게 만들 수 새 데이터베이스 사용 하도록 설정 하려면 확장 합니다. | ***전문가*** -온-프레미스 SQL Server와 호환 되는 기능. -SQL Server를 구현할 수 [AlwaysOn 통해 고가용성](https://www.microsoft.com/sqlserver/solutions-technologies/mission-critical-operations/high-availability.aspx) 2 + Vm, VM 수준의 SLA와에서 합니다. -SQL 관리 되는 방식을 완전히 제어할이 되었습니다. -SQL 라이선스 수 있으며, 하나에 대 한 시간당 비용을 지불를 다시 사용 수 있습니다. -좋은 적은 처리 하기 위한 좋아지지만 (1 t B +) 데이터베이스입니다. |
| **Cons** -온-프레미스 SQL Server에 비해 간격 일부 기능 (부족 [CLR 통합](https://technet.microsoft.com/library/ms131102.aspx), [TDE](https://technet.microsoft.com/library/bb934049.aspx), [압축 지원](https://technet.microsoft.com/library/cc280449.aspx), [SQL Reporting Services 서버](https://technet.microsoft.com/library/ms159106.aspx)등)-500GB의 데이터베이스 크기 제한 합니다. | ***Cons*** -업데이트/패치 (OS 및 SQL)는 사용자의 책임-생성 및 Db의 관리 사용자의 책임-디스크 IOPS (초당 입/출력 작업) (16 데이터 드라이브)를 통해 약 8000로 제한 됩니다. |

SQL Server VM에 사용 하려는 경우 사용자 고유의 SQL Server 라이선스를 사용할 수 있습니다 또는 시간 단위로 하나에 대 한 대금을 지불할 수 있습니다. 예를 들어 포털에서 또는 REST API를 통해 SQL Server 이미지를 사용 하 여 새 VM을 만들 수 있습니다.

![SQL server VM 만들기](data-storage-options/_static/image16.png)

![SQL Server VM 이미지의 목록](data-storage-options/_static/image17.png)

만들면 VM 할당할 우리는 SQL Server 이미지와 함께 SQL Server 라이선스 비용 VM의 사용량을 기준으로 합니다. 두 달에 대 한 실행 예정일 뿐 이라고 하는 프로젝트, 있는 경우에 1 시간으로 지불 비용이 저렴 합니다. 프로젝트 하려는 마지막 연도 대 한 생각 되 면에 일반적으로 수행 하는 방법은 라이선스 구매 비용이 저렴 합니다.

## <a name="summary"></a>요약

클라우드 컴퓨팅 혼합 하는 데 유용 하 고 가장 잘 일치 데이터 저장 방법을 응용 프로그램의 요구에 맞게 합니다. 새 응용 프로그램을 작성 하는 경우 계속 응용 프로그램 증가 하는 경우에 제대로 작동 하는 접근 방식을 선택 하기 위해 여기에 나열 된 질문에 대 한 신중 하 게 생각 합니다. [다음 장에서](data-partitioning-strategies.md) 에서는 다양 한 데이터 저장소 접근 방식이 결합 하는 데 사용할 수 있는 몇 가지 분할 전략에 설명 합니다.

## <a name="resources"></a>리소스

자세한 내용은 다음 리소스를 참조하세요.

데이터베이스 플랫폼 선택:

- [확장성이 뛰어난 솔루션에 대 한 데이터 액세스: SQL, NoSQL, 및 Polyglot 지 속성을 사용 하 여](http://aka.ms/dag-doc)합니다. 전자책 (영문)에서 Microsoft Patterns and Practices 깊이에 여러 종류의 데이터를 클라우드 응용 프로그램에 사용할 수 있는 저장 합니다.
- [Microsoft Patterns and Practices-Azure 지침](https://msdn.microsoft.com/library/ff898430.aspx)합니다. 데이터 일관성 Primer, 데이터 복제 및 인덱스 테이블이 패턴, 구체화 된 뷰 패턴 동기화 지침을 참조 하십시오.
- [기준: Acid 대신](http://queue.acm.org/detail.cfm?id=1394128)합니다. 데이터 일관성 및 확장성 간 균형에 대 한 문서 수 있습니다.
- [7 주 후에 데이터베이스를 7: 최신 데이터베이스 및 NoSQL 이동에 대 한 지침](https://www.amazon.com/Seven-Databases-Weeks-Modern-Movement/dp/1934356921)합니다. Eric Redmond 및 Jim 오른쪽 Wilson의 책입니다. 현재 사용할 수 있는 데이터 저장소 플랫폼의 범위에 자신을 도입 하는 데 좋습니다.

SQL Server 및 SQL 데이터베이스 중에서 선택 합니다.

- [SQL 데이터베이스 지침에 대 한 premium 미리 보기](https://msdn.microsoft.com/library/windowsazure/dn369873.aspx)합니다. SQL Database 프리미엄와 SQL 데이터베이스 Web 및 Business edition을 통해 선택 하는 경우에 대 한 지침을 소개 합니다.
- [지침 및 제한 사항 (Azure SQL 데이터베이스)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)합니다. SQL 데이터베이스의 제한 사항에 대 한 설명서 링크 하는 포털 페이지를 포함 한 SQL Server 기능을 중심으로 SQL 데이터베이스 지원 하지 않습니다.
- [Azure 가상 컴퓨터에서 SQL Server](https://msdn.microsoft.com/library/windowsazure/jj823132.aspx)합니다. Azure에서 SQL Server를 실행 하는 방법에 대 한 설명서에 연결 하는 포털 페이지입니다.
- [Scott Guthrie의 Azure SQL 데이터베이스에 설명](https://azure.microsoft.com/documentation/videos/sql-in-azure-scottgu/)합니다. Scott Guthrie 하 여 SQL 데이터베이스에 6 분 동영상 소개 합니다.
- [응용 프로그램 패턴 및 Azure 가상 컴퓨터에서 SQL Server에 대 한 개발 전략](https://msdn.microsoft.com/library/windowsazure/dn574746.aspx)합니다.

ASP.NET 웹 응용 프로그램에서 Entity Framework 및 SQL 데이터베이스 사용

- [MVC 5를 사용 하 여 EF 6 시작](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다. EF를 사용 하 고 SQL 데이터베이스와 Azure에는 데이터베이스를 배포 하는 MVC 응용 프로그램 빌드를 안내 하는 자습서 시리즈 9 개 부분으로 구성 합니다.
- [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../../../../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)합니다. EF Code First를 사용 하 여 데이터베이스를 배포 하는 방법에 대 한 더 심층적으로 이동 하는 자습서 시리즈 12 부분으로 구성 합니다.
- [멤버 자격, OAuth, SQL 데이터베이스와 보안 ASP.NET MVC 5 앱을 Azure 웹 사이트 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)합니다. 웹 앱을 만드는 과정을 안내 하는 단계별 자습서 인증을 사용 하 여, 응용 프로그램 테이블 멤버 자격 데이터베이스에 저장, 데이터베이스 스키마를 수정 및 Azure에 앱을 배포 합니다.
- [ASP.NET 데이터 액세스 콘텐츠 맵](https://go.microsoft.com/fwlink/p/?LinkId=282414)합니다. EF 및 SQL 데이터베이스 작업에 대 한 리소스에 연결 되어 있습니다.

MongoDB를 사용 하 여 Azure에서:

- [MongoDB Azure에서 MongoLab-](http://msopentech.com/opentech-projects/mongolab-mongodb-on-windows-azure/)합니다. MongoDB Azure에서 실행 하는 방법에 대 한 설명서에 대 한 포털 페이지입니다.
- [Azure의 가상 컴퓨터에서 실행 중인 MongoDB에 연결 하는 Azure 웹 사이트 만들기](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-store-data-mongodb-vm/)합니다. ASP.NET 웹 응용 프로그램의 MongoDB 데이터베이스를 사용 하는 방법을 보여 주는 단계별 자습서입니다.

HDInsight (Azure에서 Hadoop):

- [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/). 에 대 한 HDInsight 설명서 포털는 [Azure](https://azure.microsoft.com/) 웹 사이트입니다.
- [Hadoop 및 HDInsight: Azure의 빅 데이터](https://msdn.microsoft.com/magazine/dn385705.aspx)합니다. MSDN Magazine 문서, Bruno Terkaly 및 Ricardo Villalobos, Azure에서 Hadoop을 소개 합니다.
- [Microsoft Patterns and Practices-Azure 지침](https://msdn.microsoft.com/library/dn568099.aspx)합니다. MapReduce 패턴을 참조 하십시오.

>[!div class="step-by-step"]
[이전](single-sign-on.md)
[다음](data-partitioning-strategies.md)
