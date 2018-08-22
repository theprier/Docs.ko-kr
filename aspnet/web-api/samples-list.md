---
uid: web-api/samples-list
title: 웹 API 샘플 목록 | Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 09/18/2012
ms.assetid: 8cbd9d7f-7027-4390-b098-cb81a63ecd6f
msc.legacyurl: /web-api/samples-list
msc.type: content
ms.openlocfilehash: d25e0890a1b8d42cc638117f7bef9cf6457f3d75
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41827096"
---
<a name="web-api-samples-list"></a>Web API 샘플 목록
====================
## <a name="httpclient-samples"></a>HttpClient 샘플

**Bing 변환 샘플** | [VS 2012 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/BingTranslateSample)

호출 하는 방법을 보여 줍니다 합니다 [Microsoft Translator 서비스](https://msdn.microsoft.com/library/ff512419.aspx) 를 사용 하는 **HttpClient** 클래스. Microsoft Translator 서비스 API에 OAuth 토큰을 translator 서비스에 각 요청에 대 한 Azure 토큰 서버로 요청을 전송 하 여 응용 프로그램 구성 파일에 필요 합니다. 토큰 서버에서 결과 번역 서비스에 전송 된 요청에 공급 됩니다. 이 샘플을 실행 하기 전에 가져와야 합니다는 [Azure Marketplace에서 응용 프로그램 키](https://msdn.microsoft.com/library/hh454950.aspx) AccessTokenMessageHandler 샘플 클래스에 정보에서를 입력 합니다.

**Google Maps 샘플** | [상세 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/downloading-a-google-map-to-local-file.aspx) | [VS 2012 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/GoogleMapsSample)

사용 하 여 **HttpClient** Redmond, wa에서 지도 다운로드 하려면 [Google Maps API](https://developers.google.com/maps/), 로컬 파일로 저장 하 고 기본 이미지 뷰어를 엽니다.

**Twitter 클라이언트 샘플** | [상세 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/extending-httpclient-with-oauth-to-access-twitter.aspx) | [VS 2012 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/TwitterSample)

사용 하 여 간단한 Twitter 클라이언트를 작성 하는 방법을 보여 줍니다 **HttpClient**합니다. 샘플을 사용 하는 **HttpMessageHandler** 나가는에 OAuth 인증 정보를 삽입할 **HttpRequestMessage**. JSON.NET을 사용 하 여 Twitter에서 결과 읽습니다. 이 샘플을 실행 하기 전에 가져와야 합니다는 [Twitter에서 응용 프로그램 키](https://dev.twitter.com/), OAuthMessageHandler 샘플 클래스에 정보에서를 입력 합니다.

**World Bank 샘플** | [상세 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/httpclient-is-here.aspx) | [VS 2010 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/WorldBankSample/Net40) | [VS 2012 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/WorldBankSample/Net45)

JSON.NET을 사용 하 여 결과를 분석할 World Bank 데이터 사이트에서 데이터를 검색 하는 방법을 보여 줍니다.

## <a name="web-api-samples"></a>웹 API 샘플

**ASP.NET Web API를 시작 하기** | [VS 2012 원본](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)

기본 웹 HTTP GET 요청을 지 원하는 API를 만드는 방법을 보여 줍니다. 이 자습서에 대 한 소스 코드를 포함 [여 첫 번째 ASP.NET 웹 API](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)합니다.

**ASP.NET 웹 API JavaScript 시나리오 – 주석** | [VS 2012 원본](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)

ASP.NET Web API를 사용 하 여 웹 브라우저 클라이언트 지원 및 jQuery를 사용 하 여 쉽게 호출할 수 있는 Api를 빌드하는 방법을 보여 줍니다.

**Contact Manager** | [VS 2010 원본](https://code.msdn.microsoft.com/Contact-Manager-Web-API-0e8e373d)

이 샘플에서는 간단한 연락처 관리자 응용 프로그램을 빌드하려면 ASP.NET Web API를 사용 합니다. 응용 프로그램이 표시 하 고 연락처 목록을 관리 하는 ASP.NET MVC 응용 프로그램 및 Windows Phone 응용 프로그램에서 사용 되는 연락처 관리자 웹 API로 구성 됩니다.

**샘플을 일괄 처리** | [상세 설명](http://trocolate.wordpress.com/2012/07/19/mitigate-issue-260-in-batching-scenario/) | [VS 2012 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/BatchSample)

Asp.net HTTP 일괄 처리를 구현 하는 방법을 보여 줍니다. 일괄 처리는 다음 HTTP POST로 서버에 전송 되는 단일 MIME 다중 파트 엔터티 본문 내에서 여러 HTTP 요청을 넣는 구성 됩니다. 요청을 개별적으로 처리 됩니다 하 고 응답을 클라이언트에 반환 되는 다른 MIME 다중 파트 엔터티 본문에 배치 됩니다.

**콘텐츠 컨트롤러 샘플** | [상세 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/24/async-actions-in-asp-net-web-api.aspx) | [VS 2010 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/ContentControllerSample/Net40) | [VS 2012 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/ContentControllerSample/Net45)

읽기 및 쓰기 요청 및 응답 엔터티를 비동기적으로 스트림 사용 방법을 보여 줍니다. 샘플 컨트롤러에 두 가지 작업이 있습니다: 요청 엔터티 본문을 비동기적으로 읽어 로컬 파일에 저장 하는 PUT 작업과 로컬 파일의 내용을 반환 하는 GET 작업입니다.

**사용자 지정 어셈블리 확인자 샘플** | [VS 2012 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomAssemblyResolverSample)

ASP.NET Web API 컨트롤러는 동적으로 로드 된 라이브러리 어셈블리에서의 검색을 지 원하는 수정 하는 방법을 보여 줍니다. 이 샘플에서는 사용자 지정 구현 **IAssembliesResolver** 는 기본 구현을 호출 하 고 다음 기본 결과에 라이브러리 어셈블리를 추가 합니다.

**사용자 지정 미디어 유형 포맷터 샘플** | [상세 설명](https://blogs.msdn.com/b/henrikn/archive/2012/04/23/using-cookies-with-asp-net-web-api.aspx) | [VS 2010 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomMediaTypeFormatterSample)

사용 하는 사용자 지정 미디어 유형 포맷터를 만드는 방법을 보여 줍니다 합니다 **BufferedMediaTypeFormatter** 기본 클래스입니다. 이 기본 클래스는 포맷터를 사용 하는 주로 동기 읽기 쓰기 작업을 위한 것입니다. 미디어 유형 포맷터를 표시 하는 것 외에도,이 샘플의 일부로 등록 하 여 연결 하는 방법을 보여 줍니다 합니다 **HttpConfiguration** 응용 프로그램에 대 한 합니다. 것도 사용할 수는 **MediaTypeFormatter** 기본 클래스를 직접 주로 비동기를 사용 하는 포맷터 읽기 및 쓰기 작업에 대 한 합니다.

**사용자 지정 매개 변수 바인딩 예제** | [상세 설명](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx) | [VS 2010 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomParameterBinding)

정보 요청에서 작업 매개 변수를 연결 하는 방법을 결정 하는 프로세스 매개 변수 바인딩 프로세스를 사용자 지정 하는 방법을 보여 줍니다. 이 샘플에서는 Home 컨트롤러에 4 개의 작업이 있습니다.

1. BindPrincipal에서 사용자 지정 일반 보안 주체에는 HTTP GET 메시지;에서 아니라 IPrincipal 매개 변수를 바인딩하는 방법을 보여 줍니다.
2. BindCustomComplexTypeFromUriOrBody 또는 메시지 본문에서 요청 URI의 HTTP POST 메시지;에서 가져올 수 있는 복합 형식 매개 변수를 바인딩하는 방법을 보여 줍니다.
3. BindCustomComplexTypeFromUriWithRenamedProperty에서는 요청 URI의 HTTP POST 메시지;에서 제공 되는 이름이 바뀐된 속성을 복합 형식 매개 변수를 바인딩하는 방법을 보여 줍니다.
4. PostMultipleParametersFromBody; POST 메시지의 본문에서 여러 매개 변수를 바인딩하는 방법을 보여 줍니다.

**파일 업로드 샘플** | [상세 설명](https://blogs.msdn.com/b/henrikn/archive/2012/03/01/file-upload-and-asp-net-web-api.aspx) | [VS 2012 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/FileUploadSample)

파일을 업로드 하는 방법을 보여 줍니다.는 **ApiController** MIME 다중 파트 파일 업로드 및 사용 하 여 진행률 알림을 설정 하는 방법을 사용 하 여 **HttpClient** 사용 하 여 **ProgressNotificationHandler**. 컨트롤러는 HTML 파일 업로드의 콘텐츠를 비동기적으로 읽고 로컬 파일에 하나 이상의 본문 부분을 씁니다. 응답에는 업로드 된 파일 (또는 파일)에 대 한 정보가 들어 있습니다.

**파일 업로드를 Azure Blob 저장소 샘플** | [상세 설명](https://blogs.msdn.com/b/yaohuang1/archive/2012/07/02/asp-net-web-api-and-azure-blob-storage.aspx) | [VS 2012 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/AzureBlobsFileUploadSample)

이 샘플은 파일 업로드 예제와 유사 하지만 로컬 디스크에 업로드 된 파일을 저장 하는 대신 비동기적으로 파일을 업로드 [Azure Blob 저장소](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs) 사용 하 여 [Windows Azure SDK for.net](https://www.windowsazure.com/develop/net/)합니다. 또한 현재에 있는 blob을 나열 하기 위한 메커니즘을 제공 된 [Azure Blob Storage 컨테이너](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)합니다. 에 대해 실행 되는 샘플에서 사용할 수 있는 **Azure Storage 에뮬레이터** 는 Azure SDK와 함께 제공 됩니다. 있는 경우는 [Azure Storage 계정](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs), 실제 저장소 서비스에 대해 실행할 수 있습니다.

**Http 메시지 처리기 파이프라인 샘플** | [상세 설명](https://blogs.msdn.com/b/henrikn/archive/2012/08/07/httpclient-httpclienthandler-and-httpwebrequesthandler.aspx) | [VS 2010 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/HttpMessageHandlerPipelineSample)

연결 하는 방법을 보여 줍니다 **HttpMessageHandler** 모두 클라이언트에는 인스턴스 (**HttpClient**) 및 서버 (ASP.NET Web API). 이 샘플에서는 클라이언트와 서버 모두에서 동일한 처리기 사용 됩니다. 양쪽 모두에서 정확히 동일한 처리기 실행는 드물게 발생 하지만, 개체 모델에서 동일 클라이언트와 서버 쪽입니다.

**샘플을 업로드 하는 JSON** | [VS 2012 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/JsonUploadSample)

업로드에서 JSON을 다운로드 하는 방법을 보여 줍니다는 **ApiController**합니다. 샘플을 사용 하면 최소한 **ApiController** 하 고 사용 하 여 액세스 **HttpClient**합니다.

**매시업 샘플** | [상세 설명](https://blogs.msdn.com/b/henrikn/archive/2012/03/03/async-mashups-using-asp-net-web-api.aspx) | [VS 2012 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MashupSample)

내에서 여러 원격 사이트에 비동기적으로 액세스 하는 방법을 보여 줍니다.는 **ApiController** 동작 합니다. 작업 적중 될 때마다 요청은 비동기로 수행 되므로 없습니다 스레드가 차단 되도록 합니다.

**메모리 추적 샘플** | [상세 설명](https://blogs.msdn.com/b/roncain/archive/2012/04/12/tracing-in-asp-net-web-api.aspx) | [VS 2010 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MemoryTracingSample)

이 샘플 프로젝트에는 ASP.NET Web API 응용 프로그램에 사용자 지정 메모리에 추적 작성기를 설치 하는 Nuget 패키지를 만듭니다.

**MongoDB 예제** | [상세 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/19/using-web-api-with-mongodb.aspx) | [VS 2012 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MongoSample)

에 대 한 영구 저장소로 MongoDB를 사용 하는 방법을 보여 줍니다는 **ApiController**, 리포지토리 패턴을 사용 합니다.

**응답 본문 프로세서 샘플** | [VS 2012 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/ResponseEntityProcessorSample)

클라이언트에 전송 되기 전에 응답 엔터티 (즉, HTTP 응답 본문)를 로컬 파일에 복사 하 여 추가 처리는 파일에 비동기적으로 수행 하는 방법을 보여 줍니다. 샘플 구현 하는 **HttpMessageHandler** 하나를 사용 하 여 응답 엔터티 둘 다 쓰도록 자체 로컬 파일에 정상적으로 출력을 래핑합니다.

**XDocument 샘플을 업로드할** | [상세 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/push-and-pull-streams-using-httpclient.aspx) | [VS 2012 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/UploadXDocumentSample)

XDocument에 업로드 하는 방법을 보여 줍니다.는 **ApiController** 를 사용 하 여 **PushStreamContent** 하 고 **HttpClient**합니다.

**유효성 검사 샘플** | [VS 2010 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/ValidationSample)

HTTP 요청 내용을 검사 하려면 ASP.NET WebAPI에서 모델에 유효성 검사 특성을 사용 하는 방법을 보여 줍니다. 필요한 경우 프레임 워크 정의 둘 다 사용 하는 방법 및 모델에 주석을 추가 하려면 사용자 지정 유효성 검사 특성에 속성을 표시 하는 방법 및 잘못 된 모델 상태에 대 한 오류 응답을 반환 하는 방법을 보여 줍니다.

**웹 폼 샘플** | [상세 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/23/using-asp-net-web-api-with-asp-net-web-forms.aspx) | [VS 2010 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/WebFormSample)

Web Forms 프로젝트에 추가 ApiController를 보여 줍니다.

**[RestBugs 샘플](https://github.com/howarddierking/RestBugs)**

RestBugs는 단순한 버그 추적 하이퍼미디어 기반 시스템을 만들려면 ASP.NET Web API 및 새 HTTP 클라이언트 라이브러리를 사용 하는 방법을 보여 주는 응용 프로그램입니다. 샘플은 ASP.NET Web API를 사용 하 여 클라이언트와 서버 구현이 포함 됩니다. 서버는 리소스 표현을 생성 하는 사용자 지정 Razor 포맷터를 사용 합니다. 또한 샘플 하이퍼미디어 디자인을 사용 하 여 클라이언트 및 서버를 분리를 제공 하는 장점을 보여 주는 하는 node.js 서버를 제공 합니다.
