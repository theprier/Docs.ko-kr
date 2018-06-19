---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
title: 구조화 되지 않은 Blob 저장소 (Azure로 응용 프로그램 빌딩 실제 클라우드) | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드로 응용 프로그램 빌딩 Azure 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴 및 그을 수 있는 방법에 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/30/2015
ms.topic: article
ms.assetid: 9f05ccb1-2004-4661-ad8b-c370e6c09c8e
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
msc.type: authoredcontent
ms.openlocfilehash: c2c82a579feb586287c40bb82eba53c5f84afaba
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30872574"
---
<a name="unstructured-blob-storage-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="1b51e-104">구조화 되지 않은 Blob 저장소 (Azure로 응용 프로그램 빌딩 실제 클라우드)</span><span class="sxs-lookup"><span data-stu-id="1b51e-104">Unstructured Blob Storage (Building Real-World Cloud Apps with Azure)</span></span>
====================
<span data-ttu-id="1b51e-105">여 [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="1b51e-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="1b51e-106">[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="1b51e-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="1b51e-107">**실제 세계 클라우드로 응용 프로그램 빌딩 Azure** 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="1b51e-108">13 패턴에 설명 하 고 사례 수 있는 클라우드에 대 한 웹 앱을 개발 성공적으로 수행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="1b51e-109">전자책에 대 한 정보를 참조 하십시오. [첫 번째 장](introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>


<span data-ttu-id="1b51e-110">이전 장에서는 파티션 구성표에 검토 하 고 수정 응용 프로그램을 Azure 저장소 Blob 서비스 및 Azure SQL 데이터베이스의 다른 작업 데이터에서 이미지를 저장 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-110">In the previous chapter we looked at partitioning schemes and explained how the Fix It app stores images in the Azure Storage Blob service, and other task data in Azure SQL Database.</span></span> <span data-ttu-id="1b51e-111">이 장에서에서는 Blob 서비스에 심도 하 고 수정 프로젝트 코드에서 구현 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-111">In this chapter we go deeper into the Blob service and show how it's implemented in Fix It project code.</span></span>

## <a name="what-is-blob-storage"></a><span data-ttu-id="1b51e-112">Blob 저장소는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1b51e-112">What is Blob storage?</span></span>

<span data-ttu-id="1b51e-113">Azure 저장소 Blob 서비스는 클라우드에서 파일을 저장 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-113">The Azure Storage Blob service provides a way to store files in the cloud.</span></span> <span data-ttu-id="1b51e-114">Blob 서비스에 다양 한 파일을 로컬 네트워크 파일 시스템에 저장 하는 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-114">The Blob service has a number of advantages over storing files in a local network file system:</span></span>

- <span data-ttu-id="1b51e-115">확장성이 높은 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-115">It's highly scalable.</span></span> <span data-ttu-id="1b51e-116">단일 저장소 계정을 저장할 수 있는 [수백 테라바이트](https://msdn.microsoft.com/library/windowsazure/dn249410.aspx), 있으며 저장소 계정을 여러 개 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-116">A single Storage account can store [hundreds of terabytes](https://msdn.microsoft.com/library/windowsazure/dn249410.aspx), and you can have multiple Storage accounts.</span></span> <span data-ttu-id="1b51e-117">가장 큰 Azure 고객의 일부 페타바이트 수백 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-117">Some of the biggest Azure customers store hundreds of petabytes.</span></span> <span data-ttu-id="1b51e-118">Microsoft SkyDrive는 blob 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-118">Microsoft SkyDrive uses blob storage.</span></span>
- <span data-ttu-id="1b51e-119">지속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-119">It's durable.</span></span> <span data-ttu-id="1b51e-120">Blob 서비스에 저장 하는 모든 파일은 자동으로 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-120">Every file you store in the Blob service is automatically backed up.</span></span>
- <span data-ttu-id="1b51e-121">고가용성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-121">It provides high availability.</span></span> <span data-ttu-id="1b51e-122">[저장소에 대 한 SLA](https://go.microsoft.com/fwlink/p/?linkid=159705&amp;clcid=0x409) promises 99.9% 또는 99.99% 가동 시간, 지리적 중복 옵션에 따라 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-122">The [SLA for Storage](https://go.microsoft.com/fwlink/p/?linkid=159705&amp;clcid=0x409) promises 99.9% or 99.99% uptime, depending on which geo-redundancy option you choose.</span></span>
- <span data-ttu-id="1b51e-123">방금 저장 하 고 파일을 사용 하는 저장소는 실제 크기에 대해서만 지불 검색할 azure 플랫폼으로-서비스 (PaaS) 기능이 며 Azure 자동으로 설정 하 고 관리 하는 Vm의 디스크 드라이브에 필요한 모든 처리는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-123">It's a platform-as-a-service (PaaS) feature of Azure, which means you just store and retrieve files, paying only for the actual amount of storage you use, and Azure automatically takes care of setting up and managing all of the VMs and disk drives required for the service.</span></span>
- <span data-ttu-id="1b51e-124">Blob 서비스 REST API를 사용 하 여 또는 프로그래밍 언어 API를 사용 하 여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-124">You can access the Blob service by using a REST API or by using a programming language API.</span></span> <span data-ttu-id="1b51e-125">Sdk는.NET, Java, Ruby, 등에 대 한 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-125">SDKs are available for .NET, Java, Ruby, and others.</span></span>
- <span data-ttu-id="1b51e-126">Blob 서비스에 저장 하는 파일을 만들 수 있습니다 쉽게 공개적으로 사용할 수 있는 인터넷을 통해.</span><span class="sxs-lookup"><span data-stu-id="1b51e-126">When you store a file in the Blob service, you can easily make it publicly available over the Internet.</span></span>
- <span data-ttu-id="1b51e-127">권한이 있는 사용자 수 있도록 하는 서비스에 액세스 하는 Blob에 파일을 보호할 수 있습니다 또는 사용할 수 있도록 다른 사람에 게 제한 된 기간에 대 한 임시 액세스 토큰을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-127">You can secure files in the Blob service so they can accessed only by authorized users, or you can provide temporary access tokens that makes them available to someone only for a limited period of time.</span></span>

<span data-ttu-id="1b51e-128">Azure에 대 한 응용 프로그램을 작성 하 고 많은 온-프레미스 환경에서 것에서 이동 하는 파일-예: 이미지, 비디오, 데이터를 저장 하려면 언제 든 지 Pdf, 스프레드시트, 등-Blob 서비스를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-128">Anytime you're building an app for Azure and you want to store a lot of data that in an on-premises environment would go in files -- such as images, videos, PDFs, spreadsheets, etc. -- consider the Blob service.</span></span>

## <a name="creating-a-storage-account"></a><span data-ttu-id="1b51e-129">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="1b51e-129">Creating a Storage account</span></span>

<span data-ttu-id="1b51e-130">Blob 서비스를 시작 하려면 Azure에서 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-130">To get started with the Blob service you create a Storage account in Azure.</span></span> <span data-ttu-id="1b51e-131">포털에서 클릭 **새로** -- **데이터 서비스** -- **저장소** -- **빠른 생성**, 고 URL 및 데이터 센터 위치를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-131">In the portal, click **New** -- **Data Services** -- **Storage** -- **Quick Create**, and then enter a URL and a data center location.</span></span> <span data-ttu-id="1b51e-132">데이터 센터 위치는 웹 앱과 동일 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-132">The data center location should be the same as your web app.</span></span>

![저장소 계정 만들기](unstructured-blob-storage/_static/image1.png)

<span data-ttu-id="1b51e-134">콘텐츠를 저장 하려는 하 고 선택 하는 경우 기본 지역 선택은 [지리적 복제](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx#_Geo_Redundant_Storage) 옵션, Azure는 다른 지역에 거주의 서로 다른 데이터 센터에서 모든 데이터의 복제본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-134">You pick the primary region where you want to store the content, and if you choose the [geo-replication](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx#_Geo_Redundant_Storage) option, Azure creates replicas of all your data in a different data center in another region of the country.</span></span> <span data-ttu-id="1b51e-135">예를 들어 선택한 경우 미국 서 부 데이터 센터에 있지만 Azure 백그라운드에서도 되는 파일을 저장 하는 경우 미국 서 부 데이터 센터에 복사 다른 미국 데이터 센터 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-135">For example, if you choose the Western US data center, when you store a file it goes to the Western US data center, but in the background Azure also copies it to one of the other US data centers.</span></span> <span data-ttu-id="1b51e-136">Country 지역에서 재해 발생 하는 경우 데이터 여전히 안전 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-136">If a disaster happens in one region of the country, your data is still safe.</span></span>

<span data-ttu-id="1b51e-137">Azure 지역 정치적 경계에 걸쳐 데이터를 복제 하지 않을: 파일만; 미국 내에서 다른 지역으로 복제 된 사용자의 기본 위치를 미국에 있으면, 사용자의 기본 위치 오스트레일리아 이면 파일 오스트레일리아의 다른 데이터 센터에만 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-137">Azure won't replicate data across geo-political boundaries: if your primary location is in the U.S., your files are only replicated to another region within the U.S.; if your primary location is Australia, your files are only replicated to another data center in Australia.</span></span>

<span data-ttu-id="1b51e-138">물론, 만들 수 있습니다도 한 저장소 계정을 스크립트에서 명령을 실행 하 여 앞서 살펴본 것 처럼.</span><span class="sxs-lookup"><span data-stu-id="1b51e-138">Of course, you can also create a Storage account by executing commands from a script, as we saw earlier.</span></span> <span data-ttu-id="1b51e-139">저장소 계정을 만들려면 Windows PowerShell 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-139">Here's a Windows PowerShell command to create a Storage account:</span></span>

[!code-powershell[Main](unstructured-blob-storage/samples/sample1.ps1)]

<span data-ttu-id="1b51e-140">저장소 계정을 만든 후 Blob 서비스에 파일을 저장할을 즉시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-140">Once you have a Storage account, you can immediately start storing files in the Blob service.</span></span>

## <a name="using-blob-storage-in-the-fix-it-app"></a><span data-ttu-id="1b51e-141">Blob 저장소를 사용 하 여 수정 응용 프로그램에서</span><span class="sxs-lookup"><span data-stu-id="1b51e-141">Using Blob storage in the Fix It app</span></span>

<span data-ttu-id="1b51e-142">수정 응용 프로그램을 사용 하면 사진을 업로드 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-142">The Fix It app enables you to upload photos.</span></span>

![수정 작업 만들기](unstructured-blob-storage/_static/image2.png)

<span data-ttu-id="1b51e-144">클릭할 때 **는 FixIt 만들**, 응용 프로그램에서 지정 된 이미지 파일을 업로드 하 고 Blob 서비스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-144">When you click **Create the FixIt**, the application uploads the specified image file and stores it in the Blob service.</span></span>

### <a name="set-up-the-blob-container"></a><span data-ttu-id="1b51e-145">Blob 컨테이너를 설정</span><span class="sxs-lookup"><span data-stu-id="1b51e-145">Set up the Blob container</span></span>

<span data-ttu-id="1b51e-146">필요한 Blob 서비스에 파일을 저장 하기 위해는 *컨테이너* 에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-146">In order to store a file in the Blob service you need a *container* to store it in.</span></span> <span data-ttu-id="1b51e-147">Blob 서비스 컨테이너 파일 시스템 폴더에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-147">A Blob service container corresponds to a file system folder.</span></span> <span data-ttu-id="1b51e-148">방법을 살펴보았습니다 환경 만들기 스크립트는 [모든 자동화 장](automate-everything.md) 저장소 계정을 만들지만 컨테이너를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-148">The environment creation scripts that we reviewed in the [Automate Everything chapter](automate-everything.md) create the Storage account, but they don't create a container.</span></span> <span data-ttu-id="1b51e-149">따라서의 용도 `CreateAndConfigure` 의 메서드는 `PhotoService` 클래스가 존재 하지 않는 경우 컨테이너를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-149">So the purpose of the `CreateAndConfigure` method of the `PhotoService` class is to create a container if it doesn't already exist.</span></span> <span data-ttu-id="1b51e-150">이 메서드는 `Application_Start` 메서드에서 *Global.asax*합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-150">This method is called from the `Application_Start` method in *Global.asax*.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample2.cs)]

<span data-ttu-id="1b51e-151">저장소 계정 이름과 액세스 키에 저장 됩니다는 `appSettings` 의 컬렉션은 *Web.config* 파일, 및의 코드는 `StorageUtils.StorageAccount` 메서드는 연결 문자열을 작성 하 고 연결을 설정 하려면 해당 값을 사용:</span><span class="sxs-lookup"><span data-stu-id="1b51e-151">The storage account name and access key are stored in the `appSettings` collection of the *Web.config* file, and code in the `StorageUtils.StorageAccount` method uses those values to build a connection string and establish a connection:</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample3.cs)]

<span data-ttu-id="1b51e-152">`CreateAndConfigureAsync` 메서드 다음 Blob 서비스를 나타내는 개체를 만들고 Blob 서비스에서 명명 된 "이미지" 컨테이너 (폴더)를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-152">The `CreateAndConfigureAsync` method then creates an object that represents the Blob service, and an object that represents a container (folder) named "images" in the Blob service:</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample4.cs)]

<span data-ttu-id="1b51e-153">컨테이너 이름이 "이미지" 아직 없음-처음으로 새 저장소 계정-에 대 한 응용 프로그램을 실행 하면 코드 컨테이너를 만들고 공개 있도록 사용 권한을 설정 하는 true 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-153">If a container named "images" doesn't exist yet -- which will be true the first time you run the app against a new storage account -- the code creates the container and sets permissions to make it public.</span></span> <span data-ttu-id="1b51e-154">(기본적으로 새 blob 컨테이너는 private 및 저장소 계정에 액세스할 수 있는 권한을 가진 사용자만 액세스할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="1b51e-154">(By default, new blob containers are private and are accessible only to users who have permission to access your storage account.)</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample5.cs)]

### <a name="store-the-uploaded-photo-in-blob-storage"></a><span data-ttu-id="1b51e-155">저장소 Blob 저장소에 업로드 된 사진</span><span class="sxs-lookup"><span data-stu-id="1b51e-155">Store the uploaded photo in Blob storage</span></span>

<span data-ttu-id="1b51e-156">업로드 하 고 응용 프로그램 사용 하 여 이미지 파일을 저장 한 `IPhotoService` 인터페이스와 인터페이스의 구현을 `PhotoService` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-156">To upload and save the image file, the app uses an `IPhotoService` interface and an implementation of the interface in the `PhotoService` class.</span></span> <span data-ttu-id="1b51e-157">*PhotoService.cs* 파일 모든 수정 앱에서 Blob 서비스와 통신 하는 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-157">The *PhotoService.cs* file contains all of the code in the Fix It app that communicates with the Blob service.</span></span>

<span data-ttu-id="1b51e-158">다음 MVC 컨트롤러 메서드를 클릭할 때 호출 됩니다 **는 FixIt 만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-158">The following MVC controller method is called when the user clicks **Create the FixIt**.</span></span> <span data-ttu-id="1b51e-159">이 코드에서는 `photoService` 의 인스턴스를 참조는 `PhotoService` 클래스 및 `fixittask` 의 인스턴스를 참조는 `FixItTask` 새 작업에 대 한 데이터를 저장 하는 엔터티 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-159">In this code, `photoService` refers to an instance of the `PhotoService` class, and `fixittask` refers to an instance of the `FixItTask` entity class that stores data for a new task.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample6.cs?highlight=8)]

<span data-ttu-id="1b51e-160">`UploadPhotoAsync` 에서 메서드는 `PhotoService` Blob 서비스에 업로드 된 파일을 저장 하 고 새 blob을 가리키는 URL을 반환 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-160">The `UploadPhotoAsync` method in the `PhotoService` class stores the uploaded file in the Blob service and returns a URL that points to the new blob.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample7.cs)]

<span data-ttu-id="1b51e-161">와 같이 `CreateAndConfigure` 메서드를 코드는 저장소 계정에 연결 하 고 컨테이너 이미 있다고 가정 여기 점을 제외 하 고 "이미지" blob 컨테이너를 나타내는 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-161">As in the `CreateAndConfigure` method, the code connects to the storage account and creates an object that represents the "images" blob container, except here it assumes the container already exists.</span></span>

<span data-ttu-id="1b51e-162">다음 파일 확장명을 가진 새 GUID 값을 연결 하 여 업로드 하려고 합니다. 이미지에 대 한 고유 식별자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-162">Then it creates a unique identifier for the image about to be uploaded, by concatenating a new GUID value with the file extension:</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample8.cs)]

<span data-ttu-id="1b51e-163">다음 코드는 blob 개체를 만들려면 blob 컨테이너 개체 및 새로운 고유 식별자를 사용 하 여, 나타내는 파일 종류에 대해 한 다음 파일을 저장할 blob 저장소에 blob 개체를 사용 하 여 해당 개체에는 특성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-163">The code then uses the blob container object and the new unique identifier to create a blob object, sets an attribute on that object indicating what kind of file it is, and then uses the blob object to store the file in blob storage.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample9.cs)]

<span data-ttu-id="1b51e-164">마지막으로, blob 참조 하는 URL을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-164">Finally, it gets a URL that references the blob.</span></span> <span data-ttu-id="1b51e-165">이 URL 데이터베이스에 저장 되 고 업로드 된 이미지를 표시 하려면 수정 웹 페이지에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-165">This URL will be stored in the database and can be used in Fix It web pages to display the uploaded image.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample10.cs)]

<span data-ttu-id="1b51e-166">이 URL은 FixItTask 테이블의 열 중 하나로 데이터베이스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-166">This URL is stored in the database as one of the columns of the FixItTask table.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample11.cs?highlight=10)]

<span data-ttu-id="1b51e-167">데이터베이스에는 URL로만와 Blob 저장소에서 이미지를 수정 응용 프로그램 데이터베이스 작은, 확장 가능 하며 저렴 하 동안 유지 이미지는 비용이 적게 들고 테라바이트 또는 페타바이트 처리할 수 있는 저장소 인 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-167">With only the URL in the database, and images in Blob storage, the Fix It app keeps the database small, scalable, and inexpensive, while the images are stored where storage is cheap and capable of handling terabytes or petabytes.</span></span> <span data-ttu-id="1b51e-168">저장소 계정을 하나 수백 테라바이트 수정 사진 저장 하 고 사용 하는 것에 대 한 요금만 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-168">One storage account can store hundreds of terabytes of Fix It photos, and you only pay for what you use.</span></span> <span data-ttu-id="1b51e-169">따라서 첫 번째 몇 기가바이트 크기에 대 한 작은 유료 9 센트 시작할 수 있으며 추가 비트당 페니를 잘라내면에 대 한 이미지를 추가.</span><span class="sxs-lookup"><span data-stu-id="1b51e-169">So you can start off small paying 9 cents for the first gigabyte, and add more images for pennies per additional gigabyte.</span></span>

### <a name="display-the-uploaded-file"></a><span data-ttu-id="1b51e-170">업로드 된 파일을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-170">Display the uploaded file</span></span>

<span data-ttu-id="1b51e-171">수정 응용 프로그램 작업에 대 한 세부 정보를 표시 하는 경우 업로드 된 이미지 파일을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-171">The Fix It application displays the uploaded image file when it displays details for a task.</span></span>

![사진의 작업 세부 정보 해결](unstructured-blob-storage/_static/image3.png)

<span data-ttu-id="1b51e-173">이미지를 표시 하려면 작업을 수행 하는 MVC 뷰에 포함 된 `PhotoUrl` 브라우저에 보내지는 html 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-173">To display the image, all the MVC view has to do is include the `PhotoUrl` value in the HTML sent to the browser.</span></span> <span data-ttu-id="1b51e-174">웹 서버와 데이터베이스 사용 하지 않는 주기 이미지를 표시, 이미지 URL을 몇 바이트를만 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-174">The web server and the database are not using cycles to display the image, they are only serving up a few bytes to the image URL.</span></span> <span data-ttu-id="1b51e-175">다음 Razor 코드에서 `Model` 의 인스턴스를 참조 하는 `FixItTask` 엔터티 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-175">In the following Razor code, `Model` refers to an instance of the `FixItTask` entity class.</span></span>

[!code-cshtml[Main](unstructured-blob-storage/samples/sample12.cshtml?highlight=11)]

<span data-ttu-id="1b51e-176">표시 되는 페이지의 HTML을 보면 다음과 같이 결과 blob 저장소에서 이미지를 직접 가리키는 URL 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-176">If you look at the HTML of the page that displays, you see the URL pointing directly to the image in blob storage, something like this:</span></span>

[!code-cshtml[Main](unstructured-blob-storage/samples/sample13.cshtml?highlight=11)]

## <a name="summary"></a><span data-ttu-id="1b51e-177">요약</span><span class="sxs-lookup"><span data-stu-id="1b51e-177">Summary</span></span>

<span data-ttu-id="1b51e-178">수정 앱 Blob 서비스 및 SQL 데이터베이스에서 이미지 Url만에 이미지를 저장 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-178">You've seen how the Fix It app stores images in the Blob service and only image URLs in the SQL database.</span></span> <span data-ttu-id="1b51e-179">Blob 서비스를 사용 하 여 유지 SQL 데이터베이스 그렇지 않으면 것, 수직 확장 하 고 거의 무제한의 작업을 할 수 있습니다 및 많은 양의 코드를 작성 하지 않고도 수행할 수 있는 보다 훨씬 작습니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-179">Using the Blob service keeps the SQL database much smaller than it otherwise would be, makes it possible to scale up to an almost unlimited number of tasks, and can be done without writing a lot of code.</span></span>

<span data-ttu-id="1b51e-180">수백 테라바이트 저장소 계정에 있고 저장소 비용은 약 3 센트 매달 한 작은 트랜잭션 요금이 당 gigabyte에서 시작 하는 SQL 데이터베이스 저장소 보다 훨씬 더 저렴 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-180">You can have hundreds of terabytes in a storage account, and the storage cost is much less expensive than SQL Database storage, starting at about 3 cents per gigabyte per month plus a small transaction charge.</span></span> <span data-ttu-id="1b51e-181">한 최대 용량에 대 한 하지만 실제 저장 되므로 앱 확장할 준비가 되었습니다. 그러나이 있는 모든에 대해 추가 용량이 지불할 크기에 대해서만 하지 지불할 염두에서에 둬야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-181">And keep in mind that you're not paying for the maximum capacity but only for the amount you actually store, so your app is ready to scale but you're not paying for all that extra capacity.</span></span>

<span data-ttu-id="1b51e-182">에 [다음 장에서](design-to-survive-failures.md) 중요성 오류를 정상적으로 처리할 수 있는 클라우드 앱을 만드는 방법에 대해 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-182">In the [next chapter](design-to-survive-failures.md) we'll talk about the importance of making a cloud app capable of gracefully handling failures.</span></span>

## <a name="resources"></a><span data-ttu-id="1b51e-183">자료</span><span class="sxs-lookup"><span data-stu-id="1b51e-183">Resources</span></span>

<span data-ttu-id="1b51e-184">자세한 내용은 다음 리소스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-184">For more information see the following resources:</span></span>

- <span data-ttu-id="1b51e-185">[Azure BLOB 저장소에 대 한 소개](https://www.simple-talk.com/cloud/cloud-data/an-introduction-to-windows-azure-blob-storage-/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-185">[An Introduction to Azure BLOB Storage](https://www.simple-talk.com/cloud/cloud-data/an-introduction-to-windows-azure-blob-storage-/).</span></span> <span data-ttu-id="1b51e-186">Mike 목재 하 여 블로그입니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-186">Blog by Mike Wood.</span></span>
- <span data-ttu-id="1b51e-187">[.NET에서 Azure Blob 저장소 서비스를 사용 하는 방법](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-187">[How to use the Azure Blob Storage Service in .NET](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs).</span></span> <span data-ttu-id="1b51e-188">MicrosoftAzure.com 사이트에서 공식 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-188">Official documentation on the MicrosoftAzure.com site.</span></span> <span data-ttu-id="1b51e-189">컨테이너 만들고 업로드 등 blob 다운로드 하는 blob 저장소에 blob 저장소에 연결 하는 방법을 보여 주는 코드 예제에서는 뒤에 대 한 간략 한 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-189">A brief introduction to blob storage followed by code examples showing how to connect to blob storage, create containers, upload and download blobs, etc.</span></span>
- <span data-ttu-id="1b51e-190">[FailSafe: 복원 력 있는 확장 가능한 클라우드 서비스를 만드는](https://channel9.msdn.com/Series/FailSafe)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-190">[FailSafe: Building Scalable, Resilient Cloud Services](https://channel9.msdn.com/Series/FailSafe).</span></span> <span data-ttu-id="1b51e-191">Marc Mercuri, Ulrich Homann, Mark Simms 하 여 비디오 시리즈를 9 개 부분으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-191">Nine-part video series by Ulrich Homann, Marc Mercuri, and Mark Simms.</span></span> <span data-ttu-id="1b51e-192">고급 개념 및 아키텍처 원칙 매우 액세스 가능 하 고 흥미로운 방법으로 스토리 실제 고객과 Microsoft 고객 자문 팀 (CAT) 환경에서 가져온 것으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-192">Presents high-level concepts and architectural principles in a very accessible and interesting way, with stories drawn from Microsoft Customer Advisory Team (CAT) experience with actual customers.</span></span> <span data-ttu-id="1b51e-193">Azure 저장소 서비스와 blob의 토론, 에피소드 5 35:13에서 시작을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="1b51e-193">For a discussion of Azure Storage service and blobs, see episode 5 starting at 35:13.</span></span>
- <span data-ttu-id="1b51e-194">[Microsoft Patterns and Practices-Azure 지침](https://msdn.microsoft.com/library/dn568099.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-194">[Microsoft Patterns and Practices - Azure Guidance](https://msdn.microsoft.com/library/dn568099.aspx).</span></span> <span data-ttu-id="1b51e-195">참조 Valet 키 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="1b51e-195">See Valet Key pattern.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1b51e-196">[이전](data-partitioning-strategies.md)
> [다음](design-to-survive-failures.md)</span><span class="sxs-lookup"><span data-stu-id="1b51e-196">[Previous](data-partitioning-strategies.md)
[Next](design-to-survive-failures.md)</span></span>
