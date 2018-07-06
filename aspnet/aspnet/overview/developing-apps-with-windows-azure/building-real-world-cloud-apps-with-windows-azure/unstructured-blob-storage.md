---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
title: 구조화 되지 않은 Blob 저장소 (실제 클라우드 앱 빌드 azure) | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드 앱 빌드 Azure 전자책을 사용 하 여 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴과 그을 수 있는 방법을 설명 하는 중...
ms.author: aspnetcontent
ms.date: 03/30/2015
ms.assetid: 9f05ccb1-2004-4661-ad8b-c370e6c09c8e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
msc.type: authoredcontent
ms.openlocfilehash: 55937854546fe02c36b15b7141d90b4c0785f32b
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37823464"
---
<a name="unstructured-blob-storage-building-real-world-cloud-apps-with-azure"></a>구조화 되지 않은 Blob 저장소 (Azure 사용 하 여 빌드 실제 클라우드 앱)
====================
하 여 [Mike Wasson](https://github.com/MikeWasson)하십시오 [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 합니다 **실제 세계 클라우드 앱 빌드 Azure** 전자책 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴 설명 하 고 도움이 될 수 있는 사례 성공적인 클라우드를 위한 웹 앱을 개발할 수 있습니다. 전자책에 대 한 정보를 참조 하세요 [첫 번째 장에서](introduction.md)합니다.


이전 장에서 파티션 구성표를 살펴보고 고 Fix It 응용 프로그램을 Azure Storage Blob service 및 Azure SQL Database에서 다른 작업 데이터에 이미지를 저장 하는 방법을 설명 합니다. 이 장에서 자세히 Blob service로 이동 하 고 Fix It 프로젝트 코드에서 구현 하는 방법을 보여 줍니다.

## <a name="what-is-blob-storage"></a>Blob storage 란?

Azure Storage Blob service는 클라우드에서 파일을 저장 하는 방법을 제공 합니다. Blob service에 다양 한 로컬 네트워크 파일 시스템에 파일을 저장 하는 장점이 있습니다.

- 확장성이 높은 것입니다. 단일 저장소 계정에 저장할 수 있습니다 [수백 테라바이트](https://msdn.microsoft.com/library/windowsazure/dn249410.aspx), 및 여러 저장소 계정을 사용할 수 있습니다. 일부 큰 Azure 고객은 수백 개의 페타바이트 저장합니다. Microsoft SkyDrive는 blob 저장소를 사용합니다.
- 지속 됩니다. Blob service에 저장 하는 모든 파일 자동으로 백업 됩니다.
- 고가용성을 제공 합니다. 합니다 [저장소에 대 한 SLA](https://go.microsoft.com/fwlink/p/?linkid=159705&amp;clcid=0x409) 약속 99.9% 이상의 99.99% 가동 시간, 지리적 중복 옵션에 따라 선택 합니다.
- 이 기능은 플랫폼-as a service (PaaS)만 저장 하 고 파일을 사용 하는 저장소의 실제 크기에 대해서만 지불 검색 즉 azure 및 Azure 자동으로 설정 하 고 모든 Vm 및 디스크 드라이브에 필요한 관리 합니다 서비스입니다.
- Blob service REST API를 사용 하 여 또는 프로그래밍 언어 API를 사용 하 여 액세스할 수 있습니다. Sdk는.NET, Java, Ruby 및 다른 사용자가 사용할 수 있습니다.
- Blob service에 파일을 저장 하면 할 수 있습니다 쉽게이 공개적으로 사용할 수 있는 인터넷을 통해.
- 서비스 할 수 있는 권한이 있는 사용자만 액세스할 Blob에서 파일을 보호할 수 있습니다 또는 수 있는 사용 가능한 다른 사람에 게 제한 된 기간에 대해서만 임시 액세스 토큰을 제공할 수 있습니다.

Azure에 대 한 앱을 빌드하는 많은 온-프레미스 환경에서 비디오, 이미지와 같은 파일에서 이동 하는 데이터를 저장 하려면 언제 든 지 Pdf, 스프레드시트, 등-Blob service를 고려 합니다.

## <a name="creating-a-storage-account"></a>저장소 계정 만들기

Blob service를 사용 하 여 시작 하려면 Azure에서 저장소 계정을 만듭니다. 포털에서 클릭 **새로 만들기** -- **Data Services** -- **Storage** -- **빨리 만들기**, 고 URL 및 데이터 센터 위치를 입력 합니다. 데이터 센터 위치는 웹 앱으로 동일 해야 합니다.

![저장소 계정 만들기](unstructured-blob-storage/_static/image1.png)

콘텐츠를 저장 하려는 선택한 경우 주 지역을 선택 합니다 [함깨 geo-replication](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx#_Geo_Redundant_Storage) 옵션, Azure는 국가 다른 지역의 다른 데이터 센터의 모든 데이터의 복제본을 만듭니다. 예를 들어, 선택한 경우 미국 서 부 데이터 센터에 있지만 Azure에서 백그라운드로 이동 하는 파일을 저장 하는 경우 미국 서 부 데이터 센터에 복사 다른 미국 데이터 센터 중 하나입니다. 국가 지역에서 재해 경우 데이터가 여전히 안전 하 게 됩니다.

Azure 학적 경계에 걸쳐 데이터를 복제 되지 않습니다: 파일에는 미국; 내에서 다른 지역에만 복제 됩니다 기본 위치에 있는 경우 미국 기본 위치 오스트레일리아 이면 파일만 오스트레일리아에서 다른 데이터 센터로 복제 됩니다.

물론, 또한 만들면 저장소 계정을 스크립트에서 명령을 실행 하 여 앞에서 살펴본 것 처럼 됩니다. 다음은 저장소 계정을 만들려면 Windows PowerShell 명령:

[!code-powershell[Main](unstructured-blob-storage/samples/sample1.ps1)]

저장소 계정을 만든 후 Blob service에 파일을 저장할을 즉시 시작할 수 있습니다.

## <a name="using-blob-storage-in-the-fix-it-app"></a>Fix It 응용 프로그램에서 Blob 저장소 사용

Fix It 응용 프로그램을 사용 하면 사진 업로드 수 있습니다.

![Fix It 작업 만들기](unstructured-blob-storage/_static/image2.png)

클릭 하면 **는 FixIt 만들기**, 응용 프로그램이 지정된 된 이미지 파일을 업로드 하 고 Blob service에 저장 합니다.

### <a name="set-up-the-blob-container"></a>Blob 컨테이너 설정

필요한 Blob service에 파일을 저장 하기 위해를 *컨테이너* 에 저장 합니다. Blob service 컨테이너 파일 시스템 폴더에 해당합니다. 에서는에서 검토 하는 환경 생성 스크립트를 [장 모든 자동화](automate-everything.md) 저장소 계정을 만들지만 컨테이너를 만들지 않으므로. 따라서의 목적은 합니다 `CreateAndConfigure` 메서드의 `PhotoService` 클래스는 이미 존재 하지 않는 경우 컨테이너를 만들려고 합니다. 이 메서드는 호출을 `Application_Start` 의 메서드 *Global.asax*합니다.

[!code-csharp[Main](unstructured-blob-storage/samples/sample2.cs)]

저장소 계정 이름과 액세스 키에 저장 됩니다는 `appSettings` 의 컬렉션을 *Web.config* 파일 및 코드를 `StorageUtils.StorageAccount` 메서드 해당 값을 사용 하 여 연결 문자열을 작성 하 고 연결을 설정 하려면:

[!code-csharp[Main](unstructured-blob-storage/samples/sample3.cs)]

`CreateAndConfigureAsync` 메서드 다음 Blob service를 나타내는 개체를 만들고 Blob service의 명명 된 "이미지" 컨테이너 (폴더)를 나타내는 개체입니다.

[!code-csharp[Main](unstructured-blob-storage/samples/sample4.cs)]

컨테이너 이름이 "이미지" 아직-는 처음-새 저장소 계정에 대해 앱을 실행 하면 코드 컨테이너를 만들고 일반에 공개 하는 권한을 설정 하는 true가 됩니다. (기본적으로 새 blob 컨테이너는 전용 및 저장소 계정에 액세스할 수 있는 권한을 가진 사용자만 액세스할 수 있습니다.)

[!code-csharp[Main](unstructured-blob-storage/samples/sample5.cs)]

### <a name="store-the-uploaded-photo-in-blob-storage"></a>Blob 저장소에 업로드 한 사진 저장

업로드 하 고 앱에서는 이미지 파일을 저장 하는 `IPhotoService` 인터페이스 및 인터페이스를 구현 합니다 `PhotoService` 클래스입니다. 합니다 *PhotoService.cs* 파일 Fix It 앱에서 Blob service와 통신 하는 코드를 모두 포함 되어 있습니다.

다음 MVC 컨트롤러 메서드는 사용자가 클릭할 때 **는 FixIt 만들기**합니다. 이 코드에서는 `photoService` 의 인스턴스를 참조 하는 `PhotoService` 클래스 및 `fixittask` 의 인스턴스를 참조 하는 `FixItTask` 새 작업에 대 한 데이터를 저장 하는 엔터티 클래스입니다.

[!code-csharp[Main](unstructured-blob-storage/samples/sample6.cs?highlight=8)]

합니다 `UploadPhotoAsync` 의 메서드는 `PhotoService` 클래스 Blob service에 업로드 된 파일을 저장 하 고 새 blob을 가리키는 URL을 반환 합니다.

[!code-csharp[Main](unstructured-blob-storage/samples/sample7.cs)]

와 같이 `CreateAndConfigure` 메서드 코드를 저장소 계정에 연결 및 컨테이너가 이미 가정 여기 점을 제외 하 고 "이미지" blob 컨테이너를 나타내는 개체를 만듭니다.

그런 다음 파일 확장명을 사용 하 여 새 GUID 값을 연결 하 여 업로드할 이미지에 대 한 고유 식별자를 만듭니다.

[!code-csharp[Main](unstructured-blob-storage/samples/sample8.cs)]

다음 코드는 blob 컨테이너 개체와 새 고유 식별자를 사용 하 여 blob 개체를 만듭니다, 그리고 나타내는 파일의 종류를 하 고 파일을 저장할 blob 저장소에 blob 개체를 사용 하 여 해당 개체에서 특성을 설정 합니다.

[!code-csharp[Main](unstructured-blob-storage/samples/sample9.cs)]

마지막으로 blob을 참조 하는 URL을 가져옵니다. 이 URL에는 데이터베이스에 저장 됩니다 및 업로드 된 이미지를 표시 하려면 Fix It 웹 페이지에서 사용할 수 있습니다.

[!code-csharp[Main](unstructured-blob-storage/samples/sample10.cs)]

이 URL은 FixItTask 테이블의 열 중 하나로 데이터베이스에 저장 됩니다.

[!code-csharp[Main](unstructured-blob-storage/samples/sample11.cs?highlight=10)]

데이터베이스의 URL만을 Blob storage에 이미지를 사용 하 여 Fix It 응용 프로그램 데이터베이스 작은, 확장 가능 하며 저렴 하 반면 유지 여기서 저장소는 저렴 하 고 테라바이트 또는 페타바이트 단위로 처리할 수 있는 이미지 저장 됩니다. 저장소 계정이 수백 테라바이트 급 Fix It 사진 저장 하 고 사용한 만큼만 지불 키를 누릅니다. 따라서 첫 번째 기가바이트 작은 유료 9 센트를 시작할 수 있으며 추가 기가바이트당 페니에 대 한 자세한 이미지 추가.

### <a name="display-the-uploaded-file"></a>업로드 된 파일을 표시

Fix It 응용 프로그램 작업에 대 한 세부 정보를 표시 하는 경우 업로드 된 이미지 파일을 표시 합니다.

![사진을 사용 하 여 작업 세부 정보 해결](unstructured-blob-storage/_static/image3.png)

이미지를 표시 하려면 작업을 수행 하는 MVC 뷰는 포함 된 `PhotoUrl` 브라우저로 전송 html에서 값입니다. 웹 서버 및 데이터베이스 사용 하지 않는 주기 이미지를 표시, 이미지 URL에 몇 바이트를만 처리 됩니다. 다음 Razor 코드에서 `Model` 의 인스턴스를 참조 하는 `FixItTask` 엔터티 클래스입니다.

[!code-cshtml[Main](unstructured-blob-storage/samples/sample12.cshtml?highlight=11)]

표시 된 페이지의 HTML을 보면 URL이 같은 blob storage에 이미지를 직접 가리키는 표시 됩니다.

[!code-cshtml[Main](unstructured-blob-storage/samples/sample13.cshtml?highlight=11)]

## <a name="summary"></a>요약

Fix It 응용 프로그램에서 Blob service 및 SQL database에서 이미지 Url만 이미지를 저장 하는 방법을 살펴보았습니다. Blob service를 사용 하 여는 것이 고, 그렇지는, 거의 무제한의 작업을 강화할 수 있습니다 및 많은 양의 코드를 작성 하지 않고도 수행할 수 있습니다 보다 훨씬 작은 크기 SQL 데이터베이스를 유지 합니다.

저장소 계정에 수백 테라바이트를 지정할 수 있고 저장소 비용을 약 3 센트를 더한 작은 트랜잭션 요금이 기가바이트당부터 SQL Database 저장소 보다 훨씬 비쌉니다. 및 최대 용량에 대 한 하지만 실제 저장 하므로 앱이 확장할 준비가 있지만 있는 모든에 대해 추가 용량이 지불 하지 크기에 대해서만 지불 하지 염두에서에 둡니다.

에 [다음 장에서](design-to-survive-failures.md) 클라우드 앱을 정상적으로 오류를 처리할 수 있는 과정의 중요성에 대해 알아보겠습니다.

## <a name="resources"></a>자료

자세한 내용은 다음 리소스를 참조 합니다.

- [Azure BLOB 저장소 소개](https://www.simple-talk.com/cloud/cloud-data/an-introduction-to-windows-azure-blob-storage-/)합니다. Mike Wood 블로그입니다.
- [.NET에서 Azure Blob Storage 서비스를 사용 하는 방법을](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)합니다. MicrosoftAzure.com 사이트의 공식적인 설명서입니다. 컨테이너 만들고 업로드 등 blob을 다운로드 하는 blob storage에 연결 하는 방법을 보여 주는 코드 예제에서는 뒤에 저장소 blob에 대해 간략하게 소개 합니다.
- [FailSafe: 복원 력 있는 확장 가능한 클라우드 서비스를 만드는 데](https://channel9.msdn.com/Series/FailSafe)합니다. Marc Mercuri, Ulrich Homann, Mark Simms에서 비디오 시리즈를 9 개 부분으로 구성 합니다. 고급 개념 및 아키텍처 원칙으로 실제 고객의 Microsoft 고객 자문 팀 (CAT) 환경에서 가져온 스토리를 사용 하 여 액세스 가능 하 고 흥미로운 방식으로 표시 합니다. Azure Storage 서비스와 blob의 내용은 에피소드 5 35:13부터 참조 하세요.
- [Microsoft Patterns and Practices-Azure 지침](https://msdn.microsoft.com/library/dn568099.aspx)합니다. 발레 키 패턴을 참조 하십시오.

> [!div class="step-by-step"]
> [이전](data-partitioning-strategies.md)
> [다음](design-to-survive-failures.md)
