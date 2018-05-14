# <a name="aspnet-core-response-caching-sample"></a>ASP.NET Core 응답의 캐싱 예제

이 샘플에는 ASP.NET Core의 사용 방법을 보여 줍니다. [응답 캐싱 미들웨어](https://docs.microsoft.com/aspnet/core/performance/caching/middleware)합니다.

응용 프로그램은 인덱스 페이지를 사용 하 여 응답 포함 하는 `Cache-Control` 캐싱 동작을 구성 하는 헤더입니다. 앱 설정는 `Vary` 를 경우에만 응답을 처리 하는 캐시를 구성 하는 헤더는 `Accept-Encoding` 이후의 요청 헤더에서 원래 요청 하는 일치 항목입니다.

샘플을 실행할 때 인덱스 페이지 캐시 저장 될 때까지 10 초 동안 캐시에서 제공 됩니다.
