---
uid: web-api/samples-list
title: Web API 샘플 목록 | Microsoft Docs
author: rick-anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/18/2012
ms.topic: article
ms.assetid: 8cbd9d7f-7027-4390-b098-cb81a63ecd6f
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/samples-list
msc.type: content
ms.openlocfilehash: 1e1f43bbeedfc052f0b3a3924f51b544a5a79dca
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
ms.locfileid: "28038990"
---
<a name="web-api-samples-list"></a>Web API 샘플 목록
====================
## <a name="httpclient-samples"></a>HttpClient 샘플

**Bing 번역 샘플** | [VS 2012 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet45%2fCS%2fHttpClient%2fBingTranslateSample%2fReadMe.txt)

호출 하는 방법을 보여 줍니다.는 [Microsoft Translator 서비스](https://msdn.microsoft.com/library/ff512419.aspx) 를 사용 하는 **HttpClient** 클래스입니다. Microsoft Translator 서비스 API에는 변환기 서비스에 각 요청에 대 한 토큰 Azure 서버에 요청을 전송 하 여 응용 프로그램 구성 파일에 OAuth 토큰이 필요 합니다. 결과 토큰 서버에서 번역 서비스에 전송 된 요청에 공급 됩니다. 이 샘플을 실행 하기 전에 얻어야는 [Azure Marketplace의 응용 프로그램 키](https://msdn.microsoft.com/library/hh454950.aspx) AccessTokenMessageHandler 샘플 클래스에 대 한 정보를 입력 하 고 있습니다.

**Google 지도 샘플** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/downloading-a-google-map-to-local-file.aspx) | [VS 2012 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet45%2fCS%2fHttpClient%2fGoogleMapsSample%2fReadMe.txt)

사용 하 여 **HttpClient** Redmond, wa에서 지도 다운로드 하려면 [Google 지도 API](https://developers.google.com/maps/), 로컬 파일로 저장 하 고 기본 이미지 뷰어를 엽니다.

**Twitter 클라이언트 샘플** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/extending-httpclient-with-oauth-to-access-twitter.aspx) | [VS 2012 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet45%2fCS%2fHttpClient%2fTwitterSample%2fReadMe.txt)

사용 하는 간단한 Twitter 클라이언트를 작성 하는 방법을 보여 줍니다. **HttpClient**합니다. 이 샘플에서는 사용는 **HttpMessageHandler** OAuth 인증 정보에는 나가는 삽입할 **HttpRequestMessage**합니다. JSON.NET을 사용 하 여 Twitter에서 결과 읽습니다. 이 샘플을 실행 하기 전에 얻어야는 [Twitter에서 응용 프로그램 키](https://dev.twitter.com/), OAuthMessageHandler 샘플 클래스에 대 한 정보를 입력 하 고 있습니다.

**세계 은행 샘플** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/httpclient-is-here.aspx) | [VS 2010 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet4%2fCS%2fHttpClient%2fWorldBankSample%2fReadMe.txt) | [VS 2012 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet45%2fCS%2fHttpClient%2fWorldBankSample%2fReadMe.txt)

JSON.NET 결과 구문 분석을 사용 하 여 세계 은행 데이터 사이트에서 데이터를 검색 하는 방법을 보여 줍니다.

## <a name="web-api-samples"></a>Web API 샘플

**ASP.NET Web API 시작** | [VS 2012 소스](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)

기본 웹 HTTP GET 요청을 지 원하는 API를 만드는 방법을 보여 줍니다. 이 자습서에 대 한 소스 코드가 [Your 첫 번째 ASP.NET Web API](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)합니다.

**ASP.NET 웹 API JavaScript 시나리오-주석** | [VS 2012 소스](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)

웹 브라우저 클라이언트를 지 원하는 및 jQuery를 사용 하 여 쉽게 호출할 수 있는 Api를 만들려는 ASP.NET Web API를 사용 하는 방법을 보여 줍니다.

**않아** | [VS 2010 소스](https://code.msdn.microsoft.com/Contact-Manager-Web-API-0e8e373d)

이 샘플 ASP.NET Web API를 사용 하 여 간단한 연락처 관리자 응용 프로그램을 작성 합니다. 응용 프로그램이 표시 하 고 연락처 목록을 관리 합니다. ASP.NET MVC 응용 프로그램 및 Windows Phone 응용 프로그램에서 사용 되는 연락처 manager web API 구성 됩니다.

**샘플을 일괄 처리** | [자세한 설명](http://trocolate.wordpress.com/2012/07/19/mitigate-issue-260-in-batching-scenario/) | [VS 2012 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet45%2fCS%2fWebApi%2fHostedBatchSample%2fReadMe.txt)

Asp.net HTTP 일괄 처리를 구현 하는 방법을 보여 줍니다. 일괄 처리는 다음 HTTP POST로 서버에 전송 되는 단일 MIME 다중 파트 엔터티 본문 내에서 여러 HTTP 요청에 구성 됩니다. 요청은 개별적으로 처리 하 고 응답을 클라이언트에 반환 되는 다른 MIME 다중 파트 엔터티 본문에 배치 됩니다.

**컨트롤러 샘플 콘텐츠** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/24/async-actions-in-asp-net-web-api.aspx) | [VS 2010 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet4%2fCS%2fWebApi%2fContentControllerSample%2fReadMe.txt) | [VS 2012 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet45%2fCS%2fWebApi%2fContentControllerSample%2fReadMe.txt)

읽기 및 쓰기 요청 및 응답 엔터티를 비동기적으로 스트림을 사용 하는 방법을 보여 줍니다. 샘플 컨트롤러에 두 가지 동작: 요청 엔터티 본문을 비동기적으로 읽고 로컬 파일에 저장 하는 PUT 작업 및 로컬 파일의 내용을 반환 하는 GET 작업입니다.

**사용자 지정 어셈블리 확인자 샘플** | [VS 2012 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet45%2fCS%2fWebApi%2fCustomAssemblyResolverSample%2fReadMe.txt)

ASP.NET Web API 컨트롤러는 동적으로 로드 된 라이브러리 어셈블리에서의 검색을 지원 하도록 수정 하는 방법을 보여 줍니다. 이 샘플에서는 사용자 지정 구현 **IAssembliesResolver** 기본 구현을 호출 하 고 기본 결과에 라이브러리 어셈블리를 추가 합니다.

**사용자 지정 미디어 유형 포맷터 샘플** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/04/23/using-cookies-with-asp-net-web-api.aspx) | [VS 2010 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet4%2fCS%2fWebApi%2fCustomMediaTypeFormatterSample%2fReadMe.txt)

사용 하 여 사용자 지정 미디어 유형 포맷터를 만드는 방법을 보여 줍니다는 **BufferedMediaTypeFormatter** 기본 클래스입니다. 이 기본 클래스는 포맷터를 주로 사용 동기 읽기 및 쓰기 작업을 위한 것입니다. 미디어 유형 포맷터를 보여 주는 외에,이 샘플의 일부로 등록 하 여 연결 하는 방법을 보여 줍니다는 **HttpConfiguration** 응용 프로그램에 대 한 합니다. 사용 하 여도는 **MediaTypeFormatter** 기본 클래스를 직접 주로 비동기를 사용할 수 있는 포맷터 읽기 및 쓰기 작업에 대 한 합니다.

**사용자 지정 매개 변수 바인딩 예제** | [자세한 설명](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx) | [VS 2010 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet4%2fCS%2fWebApi%2fCustomParameterBinding%2fReadMe.txt)

요청에서 정보를 작업 매개 변수에 바인딩되는 방식을 결정 하는 프로세스 매개 변수 바인딩 프로세스를 사용자 지정 하는 방법을 보여 줍니다. 이 샘플에서는 Home 컨트롤러에는 다음 4 가지 작업이 있습니다.

1. BindPrincipal에서는 HTTP GET 메시지;에서 아니라 사용자 지정 제너릭 주체에서는 IPrincipal 매개 변수를 바인딩하는 방법을 보여 줍니다.
2. BindCustomComplexTypeFromUriOrBody에서는 또는 메시지 본문에서 요청 URI는 HTTP POST 메시지;에서 가져올 수 있는 복합 유형 매개 변수를 바인딩하는 방법을 보여 줍니다.
3. BindCustomComplexTypeFromUriWithRenamedProperty에서는 오는 요청 URI는 HTTP POST 메시지;의 이름이 바뀐된 속성을 갖는 복합 유형 매개 변수를 바인딩하는 방법을 보여 줍니다.
4. PostMultipleParametersFromBody에서는 메시지 게시;에 대 한 본문에서 여러 매개 변수를 바인딩하는 방법을 보여 줍니다.

**파일 업로드 샘플** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/03/01/file-upload-and-asp-net-web-api.aspx) | [VS 2012 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet45%2fCS%2fWebApi%2fFileUploadSample%2fReadMe.txt)

파일을 업로드 하는 방법을 보여 줍니다.는 **ApiController** MIME 다중 파트 파일 업로드 및 사용 하 여 진행률 알림을 설정 하는 방법을 사용 하 여 **HttpClient** 를 사용 하 여 **ProgressNotificationHandler**. 컨트롤러는 HTML 파일 업로드의 내용을 비동기적으로 읽고 로컬 파일에 하나 이상의 본문 파트를 씁니다. 업로드 된 파일 (또는 파일)에 대 한 정보를 포함 하는 응답입니다.

**파일에 Azure Blob 저장소 샘플에 대 한 업로드가** | [자세한 설명](https://blogs.msdn.com/b/yaohuang1/archive/2012/07/02/asp-net-web-api-and-azure-blob-storage.aspx) | [VS 2012 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/61dfed023e50#Samples%2fNet45%2fCS%2fWebApi%2fAzureBlobsFileUploadSample%2fReadMe.txt)

이 샘플은 파일 업로드 샘플 유사 하지만 로컬 디스크에 업로드 된 파일을 저장 하는 대신 비동기적으로 업로드 파일을 [Azure Blob 저장소](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs) 를 사용 하 여 [Windows Azure SDK for.NET](https://www.windowsazure.com/develop/net/)합니다. 또한 현재에 있는 blob을 나열 하기 위한 메커니즘을 제공 된 [Azure Blob 저장소 컨테이너](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)합니다. 이 샘플에 대해 실행을 수행 하려면 **Azure 저장소 에뮬레이터** Azure SDK와 함께 제공 되 합니다. 있는 경우는 [Azure 저장소 계정](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)는 실제 저장소 서비스에 대해 실행할 수 있습니다.

**Http 메시지 처리기 파이프라인 샘플** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/08/07/httpclient-httpclienthandler-and-httpwebrequesthandler.aspx) | [VS 2010 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet4%2fCS%2fWebApi%2fHttpMessageHandlerPipelineSample%2fReadMe.txt)

연결 하는 방법을 보여 줍니다 **HttpMessageHandler** 모두 클라이언트에 인스턴스 (**HttpClient**) 및 서버 (ASP.NET 웹 API). 이 샘플에서는 클라이언트와 서버 모두에서 동일한 처리기 사용 됩니다. 양쪽 모두에서 정확히 동일한 처리기는 실행 드문 이지만, 개체 모델은 클라이언트와 서버 쪽에서 동일 합니다.

**JSON 업로드 샘플** | [VS 2012 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet45%2fCS%2fWebApi%2fJsonUploadSample%2fReadMe.txt)

업로드 및에서 JSON을 다운로드 하는 방법을 보여 줍니다.는 **ApiController**합니다. 이 샘플에서는 최소한의 사용 **ApiController** 하 고 액세스를 사용 하 여 **HttpClient**합니다.

**매시업 샘플** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/03/03/async-mashups-using-asp-net-web-api.aspx) | [VS 2012 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet45%2fCS%2fWebApi%2fMashupSample%2fReadMe.txt)

내에서 여러 원격 사이트를 비동기적으로 액세스 하는 방법을 보여 줍니다.는 **ApiController** 동작 합니다. 동작 적중 될 때마다 요청 비동기로 수행 되므로 스레드가 차단 되도록 합니다.

**메모리 추적 샘플** | [자세한 설명](https://blogs.msdn.com/b/roncain/archive/2012/04/12/tracing-in-asp-net-web-api.aspx) | [VS 2010 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet4%2fCS%2fWebApi%2fMemoryTracingSample%2fReadMe.txt)

이 샘플 프로젝트를 ASP.NET Web API 응용 프로그램에 사용자 지정 메모리 추적 작성기를 설치 하는 Nuget 패키지를 만듭니다.

**MongoDB 샘플** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/19/using-web-api-with-mongodb.aspx) | [VS 2012 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet45%2fCS%2fWebApi%2fMongoSample%2fReadMe.txt)

MongoDB에 대 한 영구적 저장소로 사용 하는 방법을 보여 줍니다.는 **ApiController**, 리포지토리 패턴을 사용 하 여 합니다.

**응답 본문 프로세서 샘플** | [VS 2012 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet45%2fCS%2fWebApi%2fResponseEntityProcessorSample%2fReadMe.txt)

클라이언트에 전송 되기 전에 응답 엔터티 (즉, HTTP 응답 본문)를 로컬 파일에 복사 하 고 추가 처리를 해당 파일에 대해 비동기적으로 수행 하는 방법을 보여 줍니다. 이 샘플 구현는 **HttpMessageHandler** 를 래핑하는 모두 쓰기 자체를 일반적인 방법으로 출력 되 고 로컬 파일에 응답 엔터티 하나를 사용 합니다.

**XDocument 샘플 업로드** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/push-and-pull-streams-using-httpclient.aspx) | [VS 2012 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet45%2fCS%2fWebApi%2fUploadXDocumentSample%2fReadMe.txt)

XDocument에 업로드 하는 방법을 보여 줍니다.는 **ApiController** 를 사용 하 여 **PushStreamContent** 및 **HttpClient**합니다.

**유효성 검사 샘플** | [VS 2010 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet4%2fCS%2fWebApi%2fValidationSample%2fReadMe.txt)

내용이 HTTP 요청에 ASP.NET WebAPI에서 모델 유효성 검사 특성을 사용 하는 방법을 보여 줍니다. 프레임 워크 정의 둘 다 사용 하는 방법 및 사용자 지정 유효성 검사 특성 모델에 주석을 추가 하려면 필요에 따라 속성을 표시 하는 방법 및 잘못 된 모델 상태에 대 한 오류 응답을 반환 하는 방법을 보여 줍니다.

**웹 폼 샘플** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/23/using-asp-net-web-api-with-asp-net-web-forms.aspx) | [VS 2010 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet4%2fCS%2fWebApi%2fWebFormSample%2fReadMe.txt)

Web Forms 프로젝트에 추가 하는 ApiController 보여 줍니다.

**[RestBugs 샘플](https://github.com/howarddierking/RestBugs)**

RestBugs 간단한 버그 추적 하이퍼미디어 기반 시스템을 만드는 데 ASP.NET Web API 및 새 HTTP 클라이언트 라이브러리를 사용 하는 방법을 보여 주는 응용 프로그램입니다. 이 샘플에는 ASP.NET Web API를 사용 하 여 클라이언트와 서버 구현은 포함 되어 있습니다. 서버는 사용자 지정 Razor 포맷터를 사용 하 여 리소스 표현을 생성 합니다. 또한 샘플 하이퍼미디어 디자인을 사용 하 여 클라이언트와 서버를 분리 하에서 제공 하는 이점을 설명 하기 위해 node.js 서버를 제공 합니다.

## <a name="web-api-extensions-preview-samples"></a>Web API 확장 미리 보기 샘플

**OData 쿼리 가능 샘플** | [자세한 설명](https://blogs.msdn.com/b/alexj/archive/2012/08/15/odata-support-in-asp-net-web-api.aspx) | [VS 2010 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet4%2fCS%2fWebApi%2fODataQueryableSample%2fReadMe.txt)

OData 쿼리 중 하나를 사용 하 여 ASP.NET Web API에서 제공 하는 방법을 보여 줍니다.는 `[Queryable]` 특정 특성 또는 특성을 사용 하 여는 **ODataQueryOptions** 동작을 실행 하기 전에 쿼리를 수동으로 검사할 수 있는 action 매개 변수입니다.

CustomerController [Queryable] 특성을 사용 하 여 보여주며는 OrderController ODataQueryOptions 매개 변수를 사용 하는 방법을 보여 줍니다. ResponseController는 비슷합니다는 CustomerController 하지만 가져오기 작업을 반환 하는 대신 `IEnumerable<Customer>` 반환는 **HttpResponseMessage**합니다. 따라서 추가 헤더 필드를 추가, 쿼리 기능을 계속 사용 하면서 상태 코드, 등을 조작할 수 있습니다. 이 샘플에서는 $orderby, $skip, $top, any (), all(), 및 $filter를 사용 하 여 쿼리를 보여 줍니다.

**OData 서비스 샘플** | [자세한 설명](https://blogs.msdn.com/b/alexj/archive/2012/08/15/odata-support-in-asp-net-web-api.aspx) | [VS 2010 소스](http://aspnet.codeplex.com/SourceControl/changeset/view/15dfe7e0759f#Samples%2fNet4%2fCS%2fWebApi%2fODataServiceSample%2fReadMe.txt)

이 샘플에는 세 가지 엔터티 및 세 명의 Web API 컨트롤러 구성 된 OData 서비스를 만드는 방법을 보여 줍니다. 컨트롤러는 다양 한 수준의 노출 되는 OData 기능 측면에서 기능을 제공 합니다.

이러한 요청을 처리 하 여 키 및 만들기, 가져오기는 SupplierController 쿼리를 포함 하는 기능의 하위 집합을 노출:

- /Suppliers 가져오기
- /Suppliers(key) 가져오기
- GET /Suppliers? $filter =... &amp;$orderby =... &amp;$top =... &amp;$skip =...
- POST /Suppliers

ProductsController 노출 GET, PUT, POST, 삭제 및 이러한 각 작업에 대 한 작업을 직접 구현 하 여 패치 합니다.

ProductFamilesController 풍부한 OData 서비스를 구현 하는 데 유용한 패턴을 노출 시키는 EntitySetController 기본 클래스를 활용 합니다.

OData 서비스에 사용 되는 데이터 있습니다 $metadata 문서를 노출 하는 또한 WCF 데이터 서비스 클라이언트와 $metadata 형식을 허용 하는 다른 클라이언트에서.
